---
id: hooks-overview
title: Hooks ഒറ്റനോട്ടത്തിൽ
permalink: docs/hooks-overview.html
next: hooks-state.html
prev: hooks-intro.html
---

React 16.8 ലെ പുതിയതായി ചേർക്കപ്പെട്ട ഫീച്ചർ ആണ് *Hooks*. ഇത് ഉപയോഗിച്ച് class എഴുതാതെ സ്റ്റേറ്റും മറ്റ് റീയാക്റ്റ് ഫീച്ചറുകളും ഉപയോഗിക്കാനാവും.

Hooks [backwards-compatible](/docs/hooks-intro.html#no-breaking-changes) ആണ്. ഈ അദ്ധ്യായം പരിച്ചയസമ്പന്നരായ React ഡെവലപ്പേഴ്സിന് വേണ്ടി ഉള്ള വേഗതയേറിയ ഒരു അവലോകനമാണ്. നിങ്ങൾക്ക് ആശയക്കുഴപ്പം ഉണ്ടെങ്കിൽ, ഇതുപോലുള്ള ഒരു മഞ്ഞ ബോക്സിനായി നോക്കുക

>വിശദീകരണം
>
>Hooks എന്ത് കൊണ്ട് ഉൾപ്പെടുത്തുന്നു എന്ന് അറിയുവാൻ [പ്രചോദനം](/docs/hooks-intro.html#motivation) വായിക്കാം 

**↑↑↑ ഓരോ വിഭാഗവും ഇതുപോലൊരു മഞ്ഞ ബോക്സിലാണ് അവസാനിക്കുന്നത്. അവയിൽ വിശദമായ വിവരണം ഉൾപ്പെടുത്തിയിട്ടുണ്ട്.

## 📌 State Hook {#state-hook}

ഈ ഉദാഹരണത്തിൽ ഒരു കൗണ്ടർ ഉണ്ടാകുന്നതു എങ്ങനെ എന്ന് കാണാം. ബട്ടൺ അമർത്തിയാൽ ഇപ്പോൾ ഉള്ള മൂല്യം ഒന്നു വീതം കൂടും:

```js{1,4,5}
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

ഇവിടെ നമ്മൾ ഉപയോഗിക്കുന്നത് useState എന്ന Hook ആണ്. functional component ലേക് state കൊണ്ട് വരാൻ ആണ് ഈ hook ഉപയോഗിക്കുന്നത്. re-render കൾക്കു ഇടയിലും React ഈ state ന്റെ മൂല്യം മാറാതെ സൂക്ഷിക്കും. useState function തിരികെ തരുന്നത് രണ്ടു കാര്യങ്ങൾ ആണ്: ഇപ്പോൾ ഉള്ള state ന്റെ മൂല്യവും, ആ മൂല്യത്തെ മാറ്റുവാൻ ഉള്ള function ഉം. നിങ്ങൾക്കു ഈ function ഒരു event handler ൽ നിന്നോ, മറ്റു എവിടെ നിന്നോ വിളിക്കാവുന്നത് ആണ്. പുതിയതും പഴയതും ആയ state കൂട്ടിച്ചേർക്കുന്നില്ല എന്നത് ഒഴിച്ചാൽ class components ൽ നമ്മൾ ഉപയോഗിക്കുന്ന  `this.setState` പോലെ ആണ് ഇത് പ്രവർത്തിക്കുന്നത്. (ഇവ രണ്ടും താരതമ്യപ്പെടുത്തുന്ന ഒരു ഉദ്ധരഹാരം [Using the State Hook](/docs/hooks-state.html) എന്ന അദ്ധ്യായത്തിൽ കാണാം.)

 state ന്റെ ആദ്യ മൂല്യം ആണ് `useState` function ന്റെ ഒരേ ഒരു argument. നമ്മൾ മുകളിൽ കൊടുത്ത ഉദാഹരണത്തിൽ അത് `0` ആണ്, കാരണം നമ്മളുടെ കൌണ്ടർ പൂജ്യത്തിൽ നിന്ന് ആണ് തുടങ്ങുന്നത്. `this.state`എന്നതിൽ നിന്ന് വ്യത്യാസം ആയി state ഇവിടെ ഒരു object ആകണം എന്ന് നിർബന്ധം ഇല്ല. ആദ്യത്തെ render ൽ മാത്രമേ തുടക്കത്തിൽ കൊടുക്കുന്ന മൂല്യം ഉപയോഗിക്കുക ഉള്ളു .

#### ഒന്നിലധികം state variables ഉപയോഗിക്കാൻ {#declaring-multiple-state-variables}

ഒരേ component ൽ തന്നെ പല തവണ State Hook ഉപയോഗിക്കാൻ ആവും:

```js
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

[array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring) എന്ന് അറിയപ്പെടുന്ന സിന്റാക്സ് ഉപയോഗിച്ച് നമുക്കു തിരിച്ചു കിട്ടുന്ന array ൽ ഉള്ള മൂല്യങ്ങൾക്ക് പല പേരുകൾ കൊടുക്കാം. ഈ പേരുകൾ `useState` function ഉം ആയി ബന്ധപെട്ടു വരുന്നത് അല്ല. ഇതിനു പകരം നിങ്ങൾ `useState` വിളിക്കുമ്പോഴെല്ലാം ഒരേ ക്രമത്തിൽ ആണ് വിളിക്കുന്നത് എന്ന് React അനുമാനിക്കും. ഇത് എന്ത് കൊണ്ട് ഇങ്ങനെ പ്രവർത്തിക്കുന്നത് എന്നു നമുക്കു പിന്നീട് കാണാം. 

#### പക്ഷെ, എന്താണ് Hook? {#but-what-is-a-hook}

functional components ലേക് state ഉം lifecycle hooks ഉം തരുന്ന സവിശേഷതകൾ ചേർക്കാൻ സഹായിക്കുന്ന ഒരു ഫീച്ചർ ആണ് Hooks. functions നു ഉള്ളിൽ മാത്രമേ hooks ഉപയോഗിക്കാൻ ആവുക ഉള്ളു. (നിങ്ങൾ ഇപ്പോൾ ഉള്ള components മാറ്റി എഴുതുന്നതിനു പകരം പുതിയ components ൽ Hooks ഉപയോഗികിച്ചു തുടങ്ങണം എന്നാണ് [ഞങ്ങൾ നിർദ്ദേശിക്കുന്നത്](/docs/hooks-intro.html#gradual-adoption-strategy))

React പാക്കേജിന് അകത്തു തന്നെ useState പോലെ ഉള്ള Hooks ഉണ്ട്. ഇത് അല്ലാതെ ലോജിക് പുനരുപയോഗിക്കാൻ നിങ്ങൾക്കു സ്വന്തം ആയി Hooks എഴുതുകയും ചെയ്യാം. React ൽ ഉള്ള Hooks നമുക്കു ആദ്യം നോക്കാം.

>വിശദീകരണം
>
>State Hook നെ പറ്റി കൂടുതൽ വിശദമായി പഠിക്കാൻ ഈ പേജ് നോക്കുക : [Using the State Hook](/docs/hooks-state.html).

## ⚡️ Effect Hook {#effect-hook}

നിങ്ങൾ ഡാറ്റ കൊണ്ട് വരിക, സബ്സ്ക്രിപ്ഷനുകൾ അല്ലെങ്കിൽ അല്ലെങ്കിൽ മുമ്പത്തെ പ്രതിപാദ്യ ഘടകങ്ങളിൽ നിന്ന് DOM സ്വമേധയാ മാറ്റുക തുടങ്ങിയ ഫങ്ക്ഷന്സ് ചെയ്തിട്ടുണ്ടാകും. ഈ പ്രവർത്തനങ്ങൾ "സൈഡ് ഇഫക്റ്റുകൾ" (അല്ലെങ്കിൽ "ഇഫക്റ്റുകൾ" എന്ന് ഹ്രസ്വമായി) എന്ന് ഞങ്ങൾ വിളിക്കുന്നു, കാരണം അവ മറ്റ് components നെ ബാധിക്കുന്നു എന്ന് മാത്രം അല്ല render സമയത്തു സമയത്തു ചെയാൻ ആവില്ല.

ഇങ്ങനെ ഉള്ള side effects ചെയുവാൻ ആണ് നമ്മൾ Effect Hook `useEffect` ഉപയോഗിക്കുന്നത്. `componentDidMount`, `componentDidUpdate`, `componentWillUnmount` പോലെ ഉള്ള functions ന്റെ അതേ ഉദ്ദേശം ആണ് ഇതിനും ഉള്ളത്. (`useEffect` നെ മേൽപറഞ്ഞ functions ഉം ആയി താരതമ്യം ചെയുന്ന ഒരു ഉദ്ധരഹരണം നമുക്കു [പിന്നീട് കാണാം](/docs/hooks-effect.html))

ഉദാഹരണത്തിന് ഈ component React DOM പുതിക്കിയതിനു ശേഷം ടൈറ്റിൽ മാറ്റുന്നു:

```js{1,6-10}
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

`useEffect` ഉപയോഗിക്കുന്നതിലൂടെ നമ്മൾ React ഇനോട് DOM അപ്ഡേറ്റ് ചെയ്തതിനു ശേഷം നിങ്ങൾ എഴുതിയ effect ചെയാൻ ആണ് പറയുന്നത്. Effects components ഇന് അകത്തു തന്നെ ആണ് എന്നതിനാൽ props, state എന്നിവയെ നേരിട്ടു ഉപയോഗിക്കാൻ കഴിയും. ഒരോ render function നു ശേഷവും React നിങ്ങൾ എഴുതിയ effect ചെയ്യും - ആദ്യത്തെ render ഉൾപ്പെടെ. (class lifecycles ഉം ആയി ഇത് എങ്ങനെ താരതമ്യം ചെയുന്ന എന്ന് നമുക്കു മറ്റൊരു ഉദ്ധാഹാരണത്തിൽ കാണാം: [Using the Effect Hook](/docs/hooks-effect.html).)

Effects നു അവ ചെയ്തു കഴിയുമ്പോൾ എങ്ങനെ "വൃത്തി ആക്കണം" എന്നും ഇച്ഛാനുസൃതമായി പറഞ്ഞു കൊടുക്കുവാൻ ആകും. ഇതിനായി മറ്റൊരു function റിട്ടേൺ ചെയുക മാത്രം ആണ് വേണ്ടത്. 

ഉദാഹരത്തിനു ഈ component useEffect ഉപയോഗിച്ച് ഒരു കൂട്ടുകാരന്റെ ഓൺലൈൻ സ്റ്റാറ്റസ് അറിയാൻ ഉള്ള സബ്സ്ക്രിപ്ഷൻ എടുത്തു. അത് പോലെ തന്നെ, ഈ component ഏതെങ്കിലും കാരണവശാൽ മാറുക ആണെങ്കിൽ ഉൺസബ്സ്ക്രൈബ് ചെയുവാൻ ഉള്ള function റിട്ടേൺ ചെയുന്നു:

```js{10-16}
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);

    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

In this example, React would unsubscribe from our `ChatAPI` when the component unmounts, as well as before re-running the effect due to a subsequent render. (If you want, there's a way to [tell React to skip re-subscribing](/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects) if the `props.friend.id` we passed to `ChatAPI` didn’t change.)

Just like with `useState`, you can use more than a single effect in a component:

```js{3,8}
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }
  // ...
```

Hooks let you organize side effects in a component by what pieces are related (such as adding and removing a subscription), rather than forcing a split based on lifecycle methods.

>വിശദീകരണം
>
>`useEffect` നു വേണ്ടി ഉള്ള പേജിൽ നിങ്ങൾക്കു കൂടുതൽ പഠിക്കാം : [Using the Effect Hook](/docs/hooks-effect.html).

## ✌️ Rules of Hooks {#rules-of-hooks}

Hooks are JavaScript functions, but they impose two additional rules:

* Only call Hooks **at the top level**. Don’t call Hooks inside loops, conditions, or nested functions.
* Only call Hooks **from React function components**. Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks -- your own custom Hooks. We'll learn about them in a moment.)

We provide a [linter plugin](https://www.npmjs.com/package/eslint-plugin-react-hooks) to enforce these rules automatically. We understand these rules might seem limiting or confusing at first, but they are essential to making Hooks work well.

>വിശദീകരണം
>
>ഈ പേജിൽ നിങ്ങൾക്കു ഈ നിയമങ്ങളെ പറ്റി കൂടുതൽ പഠിക്കാം: [Rules of Hooks](/docs/hooks-rules.html).

## 💡 Building Your Own Hooks {#building-your-own-hooks}

Sometimes, we want to reuse some stateful logic between components. Traditionally, there were two popular solutions to this problem: [higher-order components](/docs/higher-order-components.html) and [render props](/docs/render-props.html). Custom Hooks let you do this, but without adding more components to your tree.

Earlier on this page, we introduced a `FriendStatus` component that calls the `useState` and `useEffect` Hooks to subscribe to a friend's online status. Let's say we also want to reuse this subscription logic in another component.

First, we'll extract this logic into a custom Hook called `useFriendStatus`:

```js{3}
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

It takes `friendID` as an argument, and returns whether our friend is online.

Now we can use it from both components:


```js{2}
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

```js{2}
function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```

The state of these components is completely independent. Hooks are a way to reuse *stateful logic*, not state itself. In fact, each *call* to a Hook has a completely isolated state -- so you can even use the same custom Hook twice in one component.

Custom Hooks are more of a convention than a feature. If a function's name starts with "`use`" and it calls other Hooks, we say it is a custom Hook. The `useSomething` naming convention is how our linter plugin is able to find bugs in the code using Hooks.

You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, and probably many more we haven't considered. We are excited to see what custom Hooks the React community will come up with.

>വിശദീകരണം
>
>You can learn more about custom Hooks on a dedicated page: [Building Your Own Hooks](/docs/hooks-custom.html).

## 🔌 Other Hooks {#other-hooks}

There are a few less commonly used built-in Hooks that you might find useful. For example, [`useContext`](/docs/hooks-reference.html#usecontext) lets you subscribe to React context without introducing nesting:

```js{2,3}
function Example() {
  const locale = useContext(LocaleContext);
  const theme = useContext(ThemeContext);
  // ...
}
```

[`useReducer`](/docs/hooks-reference.html#usereducer) ഉപയോഗിച്ച് നിങ്ങൾക്കു സങ്കീർണമായ state ഒരു reducer ഉപയോഗിച്ച് എളുപ്പത്തിൽ കൈകാര്യം ചെയാം:

```js{2}
function Todos() {
  const [todos, dispatch] = useReducer(todosReducer);
  // ...
```

>വിശദീകരണം
>
>React ലെ ബിൽഡ് ഇൻ ഹോക്‌സിനെ കുറിച്ച് കൂടുതൽ അറിയാൻ ഈ പേജ് നോക്കുക:: [Hooks API Reference](/docs/hooks-reference.html).

## Next Steps {#next-steps}

Phew, that was fast! If some things didn't quite make sense or you'd like to learn more in detail, you can read the next pages, starting with the [State Hook](/docs/hooks-state.html) documentation.

You can also check out the [Hooks API reference](/docs/hooks-reference.html) and the [Hooks FAQ](/docs/hooks-faq.html).

Finally, don't miss the [introduction page](/docs/hooks-intro.html) which explains *why* we're adding Hooks and how we'll start using them side by side with classes -- without rewriting our apps.
