# Bang — Quick Tutorial (Simple & Clear)

This guide shows how to use Bang without heavy theory. You will write and run real programs in minutes.

---

## 1) Run Your First Program

Create a file `hello.bang`:

```bang
fn main() -> void {
    print "Hello, Bang";
}

main();
```

Run it:
```powershell
bang run hello.bang
```

---

## 2) Variables and Types

Bang has simple types: `int`, `bool`, `str`.

```bang
fn main() -> void {
    let x: int = 10;
    let ok: bool = true;
    let name: str = "Bang";

    print x;
    print ok;
    print name;
}

main();
```

---

## 3) If / Else

```bang
fn main() -> void {
    let score: int = 84;
    if score >= 60 {
        print "PASS";
    } else {
        print "FAIL";
    }
}

main();
```

---

## 4) While Loop

```bang
fn main() -> void {
    let i: int = 0;
    while i < 5 {
        print i;
        i = i + 1;
    }
}

main();
```

---

## 5) Functions

```bang
fn add(a: int, b: int) -> int {
    return a + b;
}

fn main() -> void {
    print add(2, 7);
}

main();
```

---

## 6) Split Code into Files (Import)

`main.bang`:
```bang
import math;

fn main() -> void {
    print add(3, 4);
}

main();
```

`math.bang`:
```bang
fn add(a: int, b: int) -> int {
    return a + b;
}
```

---

## 7) 2D Game Example (BangRender)

```bang
import bangrender;

fn main() -> void {
    bangrender.init(800, 450, "BangRender 2D");
    bangrender.fps(60);
    let t: int = 0;

    while bangrender.present() {
        bangrender.clear(20, 24, 30);
        let x: int = (t % 600) + 50;
        bangrender.rect(x, 180, 80, 80, 230, 230, 230);
        t = t + 5;
    }
}

main();
```

---

## 8) 3D Demo (BangRender3D)

```bang
import bangrender3d;

fn main() -> void {
    bangrender3d.demo();
}

main();
```

---

## 9) WebBang (WASM)

```bang
import webbang;

fn main() -> void {
    webbang.log("Hello from WebBang");
    webbang.text("WebBang is alive");
    webbang.canvas.init(300, 150);
    webbang.canvas.rect(10, 10, 120, 60, 255, 80, 80);
}

main();
```

Run in browser:
```powershell
bang web run
```
Open: `http://localhost:8000`

---

## 10) Why Bang Exists (Short)

Bang is made to be:
- Simple like a script
- Fast like a compiled language
- Powerful for games and tools
- Usable for the web via WebBang

If you can write simple logic, you can already build games and apps in Bang.

---

## 11) Common Errors

- **“Import not found”** > make sure file name exists as `<name>.bang`
- **“Type mismatch”** > check variable types
- **Web not running** > use `bang web run`

---

## 12) Next Steps

- Edit the examples in `examples/`
- Write a small game
- Try WebBang for a simple site
- Extend BangRender with new commands

---

That’s it. Bang is meant to be easy, so keep it simple and build cool things.
