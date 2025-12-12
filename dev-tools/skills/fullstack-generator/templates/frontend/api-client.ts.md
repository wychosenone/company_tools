# API Client Template

Fetch wrapper with automatic error handling and credentials.

```typescript
// src/api/client.ts

const API_BASE = import.meta.env.VITE_API_URL || 'http://localhost:3001/api';

class ApiError extends Error {
  constructor(public status: number, message: string) {
    super(message);
    this.name = 'ApiError';
  }
}

async function request<T>(
  endpoint: string,
  options: RequestInit = {}
): Promise<T> {
  const url = `${API_BASE}${endpoint}`;

  const config: RequestInit = {
    ...options,
    credentials: 'include', // Important: send cookies
    headers: {
      'Content-Type': 'application/json',
      ...options.headers,
    },
  };

  const response = await fetch(url, config);

  // Handle non-JSON responses
  const contentType = response.headers.get('content-type');
  const isJson = contentType?.includes('application/json');
  const data = isJson ? await response.json() : null;

  if (!response.ok) {
    throw new ApiError(
      response.status,
      data?.error || `Request failed with status ${response.status}`
    );
  }

  return data;
}

export const api = {
  get: <T>(endpoint: string) => request<T>(endpoint, { method: 'GET' }),

  post: <T>(endpoint: string, body?: unknown) =>
    request<T>(endpoint, {
      method: 'POST',
      body: body ? JSON.stringify(body) : undefined,
    }),

  put: <T>(endpoint: string, body?: unknown) =>
    request<T>(endpoint, {
      method: 'PUT',
      body: body ? JSON.stringify(body) : undefined,
    }),

  patch: <T>(endpoint: string, body?: unknown) =>
    request<T>(endpoint, {
      method: 'PATCH',
      body: body ? JSON.stringify(body) : undefined,
    }),

  delete: <T>(endpoint: string) => request<T>(endpoint, { method: 'DELETE' }),
};
```

## Usage Examples

```typescript
// GET request
const tasks = await api.get<Task[]>('/tasks');

// POST request
const newTask = await api.post<Task>('/tasks', {
  title: 'New task',
  dueDate: '2024-12-31',
});

// PUT request
const updated = await api.put<Task>(`/tasks/${id}`, {
  title: 'Updated title',
});

// DELETE request
await api.delete(`/tasks/${id}`);

// Error handling
try {
  await api.post('/auth/login', { email, password });
} catch (error) {
  if (error instanceof ApiError) {
    if (error.status === 401) {
      console.log('Invalid credentials');
    } else {
      console.log('Error:', error.message);
    }
  }
}
```

## Key Features

- `credentials: 'include'` sends httpOnly cookies automatically
- Type-safe with generics
- Custom ApiError class for better error handling
- Environment variable for API URL
