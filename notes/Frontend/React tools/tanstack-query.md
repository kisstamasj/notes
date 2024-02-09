# TanStack Query

Toss out that granular state management, manual refetching and endless bowls of async-spaghetti code. TanStack Query gives you declarative, always-up-to-date auto-managed queries and mutations that directly improve both your developer and user experiences.

## Install (recommended)

```npm install axios @tanstack/react-query @tanstack/react-query-devtools react-hook-form```
- dev dependencies:
```npm install @tanstack/eslint-plugin-query -D ```

## Setup

- .eslint.cjs:
```cjs
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react-hooks/recommended',
    'plugin:@tanstack/eslint-plugin-query/recommended', // <- this line needed
  ],
  ignorePatterns: ['dist', '.eslintrc.cjs'],
  parser: '@typescript-eslint/parser',
  plugins: ['react-refresh', "@tanstack/query"], // <- add tanstack query to the plugins
  rules: {
    'react-refresh/only-export-components': [
      'warn',
      { allowConstantExport: true },
    ],
  },
}
```

## Usage
- Wrap the project between QueryClientProvider:
```tsx
// default query client settings
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      retry: 5,
      retryDelay: 1000,
    }
  }
});


ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}> // -> this is the provider
      <App />
      <ReactQueryDevtools initialIsOpen={false} /> // -> react query dev tools
    </QueryClientProvider>
  </React.StrictMode>
);
```
- create `services` folder for all the api related service
- create `services/api.ts` for the api communications
```ts
// create base instance of axios
const BASE_URL = "http://localhost:8080";
const axiosInstance = axios.create({
    baseURL: BASE_URL
})

// create api requests to the backend

// Get todo ids
export const getTodosIds = async () => {
    return (await axiosInstance.get<Todo[]>("/todos")).data.map((todo) => todo.id);
}

// Get todo
export const getTodo = async (id: number) => {
    return (await axiosInstance.get<Todo>(`/todos/${id}`)).data
}

// Create todo
export const createTodo = async (data: Todo) => {
    return (await axiosInstance.post<Todo>("/todos", data)).data
}

// Update tudo
export const updateTodo = async (data: Todo) => {
    return (await axiosInstance.put<Todo>(`/todos/${data.id}`, data)).data
}
```

- create `services/queries.ts` for the queries wich will query data with the api functions
```ts
export function useTodosIds() {
  return useQuery({
    queryKey: ["todos"],
    queryFn: getTodosIds,
    refetchOnWindowFocus: false,
  });
}

export function useTodos(ids: (number | undefined)[] | undefined) {
  return useQueries({
    queries: (ids ?? []).map((id) => {
      return {
        queryKey: ["todo", { id }],
        queryFn: () => getTodo(id!),
      };
    }),
  });
}
```

- create `services/mutations.ts` for all the mutations wich will mutate data with the api functions
```ts
export function useCreateTodo() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: (data: Todo) => createTodo(data),
    onMutate: () => {
      console.log("onMutate");
    },
    onSuccess: () => {
      console.log("onSuccess");
    },
    onError: () => {
      console.log("onError");
    },
    onSettled: async (_, error) => {
      if (error) {
        console.error(error);
      } else {
        // invalidate the data will cause the data refetch
        await queryClient.invalidateQueries({ queryKey: ["todos"] });
      }
    },
  });
}

export const useUpdateTodo = () => {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: (data: Todo) => updateTodo(data),
    onMutate: ({ id }) => {
      return { id };
    },
    onSuccess: () => {
      console.log("onSuccess");
    },
    onError: () => {
      console.log("onError");
    },
    onSettled: async (_, error, variables) => {
      if (error) {
        console.error(error);
      } else {
        // invalidate the data will cause the data refetch
        await queryClient.invalidateQueries({ queryKey: ["todos"] });
        await queryClient.invalidateQueries({
          queryKey: ["todo", { id: variables?.id }],
        });
      }
    },
  });
};
```
- using in component
```tsx
export default function Todos() {
  const todosIdsQuery = useTodosIds();
  const todosQueries = useTodos(todosIdsQuery.data);
  const createTodoMutatation = useCreateTodo();
  const updateTodoMutatation = useUpdateTodo();

  const handleCreateTodo: SubmitHandler<Todo> = (data) => {
    createTodoMutatation.mutate(data);
  };
  const handleMarkAsDone: SubmitHandler<Todo> = (data) => {
    updateTodoMutatation.mutate({ ...data, checked: !data.checked });
  };

  return (
    {todosQueries.length > 0 &&
          todosQueries?.map(({ data }) => {
             return (
                <p>{data.title}</p>
              )     
          })
    }
  )
}
```




