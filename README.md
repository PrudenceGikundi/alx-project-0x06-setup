# alx-project-0x06-setup
# Counter App with useState, ContextAPI, and Redux

This project involves the progressive development of a Counter App using React's `useState` hook, ContextAPI, and Redux for state management. Each phase focuses on implementing new functionalities and improving the app's architecture.

## Project Objectives
- Build a simple counter application using React's `useState`.
- Implement ContextAPI for global state management.
- Integrate Redux to handle state in a scalable manner for larger applications.

## Setup Instructions

### Initial Setup
1. Clone the repository:
   ```bash
   git clone <repository_url>
   ```
2. Navigate to the project directory:
   ```bash
   cd alx-project-0x06
   ```
3. Install dependencies:
   ```bash
   npm install
   npm install react-icons
   npm install redux react-redux @reduxjs/toolkit
   npm install @types/react-redux
   
   ```
4. Start the development server:
   ```bash
   npm run dev
   ```
5. Open [http://localhost:3000](http://localhost:3000) in your browser to view the app.

---

## Features

### Phase 1: Counter App with `useState`
- Implemented in `pages/counter-app.tsx`.
- Tracks a counter using the `useState` hook.
- Includes Increment and Decrement buttons with dynamic messages.

**Code Highlights:**
```tsx
const [count, setCount] = useState(0);
const increment = () => setCount(count + 1);
const decrement = () => setCount(count > 0 ? count - 1 : 0);
```

---

### Phase 2: Global State with ContextAPI
- Added `context/CountContext.tsx` for global state management.
- Context provides `count`, `increment`, and `decrement` across components.
- Header displays the current count using the global state.

**Code Highlights:**
```tsx
export const CountContext = createContext<CountContextProps | undefined>(undefined);
export const CountProvider = ({ children }: { children: ReactNode }) => {
  const [count, setCount] = useState<number>(0);
  const increment = () => setCount((count) => count + 1);
  const decrement = () => setCount((count) => (count > 0 ? count - 1 : 0));

  return (
    <CountContext.Provider value={{ count, increment, decrement }}>
      {children}
    </CountContext.Provider>
  );
};
```

---

### Phase 3: Global State with Redux
- Added `store/store.ts` for Redux store configuration.
- Counter state managed via Redux Toolkit's `createSlice`.
- Integrated Redux `Provider` in `_app.tsx`.
- Both `Header` and `CounterApp` use `useSelector` to access the Redux state.

**Store Configuration:**
```tsx
const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value > 0 ? (state.value -= 1) : 0;
    },
  },
});

const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
  },
});

export const { increment, decrement } = counterSlice.actions;
export default store;
```

---

## Project Structure
```
.
├── components/
│   ├── common/
│   │   └── Button.tsx
│   └── layouts/
│       └── Header.tsx
├── context/
│   └── CountContext.tsx
├── pages/
│   ├── 404.tsx
│   ├── _app.tsx
│   ├── _document.tsx
│   ├── counter-app.tsx
│   └── index.tsx
├── store/
│   └── store.ts
├── styles/
│   └── globals.css
└── README.md

```

---

## How to Test
1. Run the app:
   ```bash
   npm run dev
   ```
2. Open [http://localhost:3000](http://localhost:3000).
3. Navigate to the Counter App page.
4. Use the Increment and Decrement buttons to modify the counter.
5. Verify that the counter updates in both the `Header` and `CounterApp` components.

---

## Dependencies
- **React**: Frontend library.
- **Next.js**: Framework for server-side rendering.
- **Redux**: State management library.
- **Tailwind CSS**: Utility-first CSS framework.

---

## Author
Prudence Kendi

---

## License
This project is licensed under the MIT License.
