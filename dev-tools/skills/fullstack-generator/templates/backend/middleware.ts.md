# Auth Middleware Template

JWT verification middleware to protect routes.

```typescript
// src/middleware/auth.ts

import { Request, Response, NextFunction } from 'express';
import jwt from 'jsonwebtoken';
import { prisma } from '../lib/prisma';

// Extend Express Request type
declare global {
  namespace Express {
    interface Request {
      userId?: string;
      user?: {
        id: string;
        email: string;
        name: string;
      };
    }
  }
}

// Basic auth check - just verifies token
export const requireAuth = async (
  req: Request,
  res: Response,
  next: NextFunction
) => {
  try {
    const { accessToken } = req.cookies;

    if (!accessToken) {
      return res.status(401).json({ error: 'Authentication required' });
    }

    const payload = jwt.verify(accessToken, process.env.JWT_SECRET!) as {
      userId: string;
    };

    req.userId = payload.userId;
    next();
  } catch (error) {
    return res.status(401).json({ error: 'Invalid or expired token' });
  }
};

// Full auth check - verifies token and loads user
export const requireAuthWithUser = async (
  req: Request,
  res: Response,
  next: NextFunction
) => {
  try {
    const { accessToken } = req.cookies;

    if (!accessToken) {
      return res.status(401).json({ error: 'Authentication required' });
    }

    const payload = jwt.verify(accessToken, process.env.JWT_SECRET!) as {
      userId: string;
    };

    const user = await prisma.user.findUnique({
      where: { id: payload.userId },
      select: { id: true, email: true, name: true },
    });

    if (!user) {
      return res.status(401).json({ error: 'User not found' });
    }

    req.userId = user.id;
    req.user = user;
    next();
  } catch (error) {
    return res.status(401).json({ error: 'Invalid or expired token' });
  }
};

// Optional auth - doesn't fail if no token, just sets user if valid
export const optionalAuth = async (
  req: Request,
  res: Response,
  next: NextFunction
) => {
  try {
    const { accessToken } = req.cookies;

    if (accessToken) {
      const payload = jwt.verify(accessToken, process.env.JWT_SECRET!) as {
        userId: string;
      };
      req.userId = payload.userId;
    }

    next();
  } catch (error) {
    // Token invalid, but continue without user
    next();
  }
};
```

## Usage in Routes

```typescript
import { Router } from 'express';
import { requireAuth, requireAuthWithUser } from '../middleware/auth';

const router = Router();

// Protected route - user must be logged in
router.get('/tasks', requireAuth, async (req, res) => {
  const tasks = await prisma.task.findMany({
    where: { userId: req.userId },
  });
  res.json(tasks);
});

// Route that needs user data
router.get('/profile', requireAuthWithUser, async (req, res) => {
  res.json({ user: req.user });
});

export default router;
```
