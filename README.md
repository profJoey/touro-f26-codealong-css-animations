## **Code-Along: CSS Animations**

### **What We're Building**

A page full of boxes that move, change color, spin, bounce, and pulse — all with CSS. No JavaScript.

We'll learn three tools, in order:

1. **Transitions** — smooth changes between two states (like on hover)
2. **Transforms** — moving, rotating, and scaling things
3. **Keyframes** — animations that run on their own, with as many steps as you want

---

### **Getting Set Up**

**1\. Click the green "Use this template" button**

**2\. Name your repository:** `touro-f26-codealong-css-animations-lastname-firstname`

**3\. Click "Create repository from template"**

**4\. Click the green "Code" button → "Create Codespace"** and wait for it to boot.

**5\. Open a preview of `index.html`** so you can see your changes as you go.

---

### **The Files**

| File | What it is |
| --- | --- |
| `index.html` | The page with all the boxes. **You won't edit this** (except for one line, below). |
| `style.css` | **Your file.** It has comments marking where each step goes. |
| `completed-style.css` | The finished answer. Peek at it if you get stuck. |

**Want to see the finished result first?** In `index.html`, find this line:

```html
<link rel="stylesheet" href="style.css">
```

Change `style.css` to `completed-style.css`, save, and look at the page. **Change it back to `style.css` before you start coding**, or you won't see your own work.

Every box has two classes: `box` (the blue square, already styled) and a step class like `step1`. You'll write CSS for the step classes.

---

## **Part 1: Transitions**

> **The big idea:** A transition needs a **trigger** — something that changes the element from state A to state B. We'll use `:hover`. The transition makes the change smooth instead of instant.

### **Step 1: Your first transition**

First, just change the color on hover:

```css
.step1:hover {
  background-color: tomato;
}
```

Hover over box 1. The color *snaps* instantly. Now add a transition to the box itself (not the hover):

```css
.step1 {
  transition: background-color 0.3s;
}
```

Hover again. Now it fades. `transition` says: *"when this property changes, take 0.3 seconds to do it."*

> **Why on `.step1` and not `.step1:hover`?** If it's on the normal state, the animation runs both ways — when you hover *and* when you leave.

### **Step 2: Animate more than one thing**

```css
.step2 {
  transition: all 0.3s;
}

.step2:hover {
  transform: scale(1.2);
  border-radius: 50%;
}
```

`all` means "animate every property that changes." The box grows and becomes a circle at the same time.

### **Step 3: Timing functions**

A timing function controls the *feel* of the motion — does it speed up, slow down, or stay steady?

```css
.step3a { transition: transform 1s ease; }
.step3b { transition: transform 1s linear; }
.step3c { transition: transform 1s ease-in-out; }

.step3a:hover,
.step3b:hover,
.step3c:hover {
  transform: translateY(80px);
}
```

Hover over each of the three boxes and compare:

- `ease` — starts fast, slows down at the end (the default)
- `linear` — same speed the whole time (feels robotic)
- `ease-in-out` — slow start, slow end (feels natural)

### **Step 4: Delay**

```css
.step4 {
  transition: background-color 0.3s;
  transition-delay: 0.5s;
}

.step4:hover {
  background-color: seagreen;
}
```

Hover and wait — the change starts half a second later.

---

## **Part 2: Transforms**

> **The big idea:** `transform` moves, rotates, or resizes an element **without pushing other elements around**. Animating `transform` (and `opacity`) is also the smoothest kind of animation for the browser. Use them whenever you can.

### **Step 5: translate, rotate, scale**

```css
.step5a,
.step5b,
.step5c {
  transition: transform 0.3s;
}

.step5a:hover { transform: translateX(20px); }
.step5b:hover { transform: rotate(45deg); }
.step5c:hover { transform: scale(1.3); }
```

- `translateX(20px)` — slides right 20px (`translateY` moves up/down)
- `rotate(45deg)` — turns 45 degrees
- `scale(1.3)` — grows to 130% size

### **Step 6: Combine them — the "lift" card**

You can put several transforms in one line, separated by spaces:

```css
.step6 {
  transition: transform 0.3s, box-shadow 0.3s;
}

.step6:hover {
  transform: translateY(-10px) rotate(5deg);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
}
```

The box lifts up, tilts, and gets a shadow — like picking up a card. You'll see this effect all over real websites.

> **Careful:** Only **one** `transform` line works per rule. If you write two, the second one replaces the first. Combine them on one line instead.

---

## **Part 3: Keyframes**

> **The big idea:** Keyframes don't need a trigger. They run as soon as the page loads. You describe the steps of the animation with `@keyframes`, give it a name, then attach that name to an element.

### **Step 7: Your first @keyframes — fade in**

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

.step7 {
  animation-name: fadeIn;
  animation-duration: 2s;
}
```

Refresh the page. The box fades in over 2 seconds.

Two parts, always:

1. **`@keyframes fadeIn`** — defines the animation (you make up the name)
2. **`animation-name: fadeIn`** — puts it on an element

### **Step 8: Percent steps — bounce**

`from` and `to` only give you two steps. Percentages let you add as many as you want:

```css
@keyframes bounce {
  0%   { transform: translateY(0); }
  50%  { transform: translateY(-40px); }
  100% { transform: translateY(0); }
}

.step8 {
  animation-name: bounce;
  animation-duration: 1s;
  animation-iteration-count: infinite;
}
```

The box goes up halfway through, then comes back down. `infinite` makes it repeat forever.

> `from` is the same as `0%`, and `to` is the same as `100%`.

### **Step 9: Going back and forth — alternate**

```css
@keyframes pulse {
  from { transform: scale(1); }
  to   { transform: scale(1.2); }
}

.step9 {
  animation-name: pulse;
  animation-duration: 0.8s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```

`alternate` plays the animation forward, then backward, then forward... so it grows and shrinks smoothly instead of jumping back to the start.

### **Step 10: The shorthand**

Writing four `animation-` lines gets long. You can put them all on one line:

```css
@keyframes wiggle {
  0%   { transform: rotate(0deg); }
  25%  { transform: rotate(10deg); }
  75%  { transform: rotate(-10deg); }
  100% { transform: rotate(0deg); }
}

.step10 {
  animation: wiggle 0.5s ease-in-out infinite;
}
```

The order to remember: **name → duration → timing → how many times**.