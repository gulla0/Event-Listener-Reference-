# 📌 Event Listener Cheat Sheet in React

This guide helps you decide **when to use `useEffect` for event listeners in React**.

---

## 🗺️ Where Is the Event Happening?

| **Where?**                                   | **Example**                                | **useEffect Needed?** | **Why?**                                                                                       |
|-----------------------------------------------|--------------------------------------------|----------------------|------------------------------------------------------------------------------------------------|
| Inside JSX (React-managed)                    | `<button onClick={handleClick} />`         | ❌ No                | React attaches/removes handlers for you when elements mount/unmount.                           |
| DOM element you control (via `ref`)           | `ref.current.addEventListener("scroll", ...)` | ✅ Yes               | You must attach/remove the listener manually in `useEffect` (and clean up on unmount).         |
| Global objects (`window`, `document`)         | `window.addEventListener("resize", ...)`   | ✅ Yes               | React doesn’t manage these. Use `useEffect` and remove in cleanup to avoid leaks.              |
| External APIs / libraries (WebSocket, etc.)   | `socket.on("message", ...)`                | ✅ Yes               | You need to subscribe/unsubscribe when the component mounts/unmounts.                          |
| Timers (`setInterval`, `setTimeout`)          | `setInterval(doSomething, 1000)`           | ✅ Yes               | Use `useEffect` to start/stop timers and clean up with `clearInterval`/`clearTimeout`.         |
| React state or prop handlers                  | `onChange={setValue}`                      | ❌ No                | Auto-cleaned up when the component re-renders/unmounts.                                        |

---

## ✅ Example: Good Practice (Global Event)

```jsx
useEffect(() => {
  const handler = () => console.log("Window resized!");
  window.addEventListener("resize", handler);

  return () => {
    window.removeEventListener("resize", handler); // cleanup
  };
}, []);
```
- **Adds the event listener when component mounts**
- **Removes the listener when component unmounts (cleanup)**

---

## ❌ Example: Bad Practice (Causes Leaks)

```jsx
function MyComp() {
  // This runs every render — BAD
  window.addEventListener("resize", () => console.log("resized"));
  return <div>Hello</div>;
}
```

- Adds a new listener **every render**
- **Never cleaned up**
- **Memory leak** plus **duplicate logs**

---

## 🔑 Rule of Thumb

- 👉 **If React can see the event in JSX, _no_ `useEffect`.**
- 👉 **If the event is outside React’s world (global objects, external APIs, timers), _always_ use `useEffect` with cleanup.**

---

## 💡 Want More?

Would you like to see how to wrap this pattern into a custom hook (like `useWindowResize`) so you never repeat this boilerplate again?
