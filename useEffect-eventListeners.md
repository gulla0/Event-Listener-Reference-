📌 Event Listener Cheat Sheet in React

Where is the event happening?	Example	Do you need useEffect?	Why
Inside JSX (React-managed)	<button onClick={handleClick} />	❌ No	React attaches/removes handlers for you when elements mount/unmount.
DOM element you control (via ref)	ref.current.addEventListener("scroll", ...)	✅ Yes	You must attach the listener manually in useEffect and clean it up when the element unmounts.
Global objects (window, document)	window.addEventListener("resize", ...)	✅ Yes	React doesn’t manage these. You must add in useEffect and remove in cleanup to avoid leaks.
External APIs / libraries (WebSocket, Firebase, etc.)	socket.on("message", ...)	✅ Yes	Same idea: you need to subscribe/unsubscribe when component mounts/unmounts.
Timers (setInterval, setTimeout)	setInterval(doSomething, 1000)	✅ Yes	Use useEffect to start it and return cleanup with clearInterval/clearTimeout.
React state or prop handlers	onChange={setValue}	❌ No	These are automatically cleaned up when the component re-renders/unmounts.


⸻

✅ Example of good practice (global event)

useEffect(() => {
  const handler = () => console.log("Window resized!");
  window.addEventListener("resize", handler);

  return () => {
    window.removeEventListener("resize", handler); // cleanup
  };
}, []);


⸻

❌ Example of bad practice (causes leaks)

function MyComp() {
  // This runs every render — BAD
  window.addEventListener("resize", () => console.log("resized"));
  return <div>Hello</div>;
}

	•	Adds a new listener every render.
	•	Never cleaned up.
	•	Memory leak + duplicate logs.

⸻

🔑 Rule of thumb to remember:

👉 If React can see the event in JSX, no useEffect.
👉 If the event is outside React’s world (global objects, external APIs, timers), always use useEffect with cleanup.

⸻

Would you like me to also show how this looks if we wrap it into a custom hook (like useWindowResize) so you never repeat this boilerplate again?
