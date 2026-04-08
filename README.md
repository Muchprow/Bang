# Bang Language — Documentation

Bang is a lightweight, fast language designed for games, utilities, and web apps. This document explains how to write code, run programs, and use the built?in libraries.

## 1) Quick Start

### 1.1 Install/Run (local dev)

```powershell
cd D:\Bang\bang
$env:CARGO_TARGET_DIR="d:\Bang\target"

# Run a file
cargo run --bin bang -- run examples\01_language.bang

# Install bang.exe to PATH
cargo run --bin bang -- install --path
```

After installation:

```powershell
bang run examples\01_language.bang
```

### 1.2 Project Structure

A minimal project:
```
MyGame/
  main.bang
  bang.toml
```

Create one quickly:
```powershell
bang new MyGame
```

## 2) Language Basics

### 2.1 Variables and Types

Types: `int`, `bool`, `str`, `void`

```bang
let x: int = 10;
let ok: bool = true;
let msg: str = "hello";
```

### 2.2 Expressions and Operators

Arithmetic: `+ - * / %`
Comparison: `== != < <= > >=`
Boolean: `!` (not)

```bang
let a: int = 7;
let b: int = 3;
print a + b * 2;
print a % b;
print a > b;
```

### 2.3 Functions

```bang
fn add(a: int, b: int) -> int {
    return a + b;
}

fn main() -> void {
    print add(2, 5);
}

main();
```

### 2.4 If / Else

```bang
fn main() -> void {
    let x: int = 12;
    if x > 10 {
        print 1;
    } else {
        print 0;
    }
}

main();
```

### 2.5 While Loop

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

### 2.6 Imports

Imports load other `.bang` files by name.

`main.bang`:
```bang
import math;

fn main() -> void {
    print add(4, 7);
}

main();
```

`math.bang`:
```bang
fn add(a: int, b: int) -> int {
    return a + b;
}
```

Search order:
1. Current file folder
2. Project folder
3. `project/std/`
4. `engine/std/` (Bang built?ins)

## 3) Running and Building

### 3.1 Run a file
```powershell
bang run examples\01_language.bang
```

### 3.2 Build EXE
```powershell
bang build D:\MyGame
```
Output:
```
D:\MyGame\build\MyGame.exe
```

## 4) BangRender (2D)

**BangRender** is the built?in 2D rendering library.

### 4.1 2D Example
File: `examples\03_bangrender_2d.bang`

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

### 4.2 BangRender API
- `bangrender.init(w:int, h:int, title:str)`
- `bangrender.clear(r:int, g:int, b:int)`
- `bangrender.rect(x:int, y:int, w:int, h:int, r:int, g:int, b:int)`
- `bangrender.present() -> bool`
- `bangrender.fps(n:int)` (limit FPS)

## 5) BangRender 3D

**BangRender3D** is the 3D pipeline based on `wgpu`.

### 5.1 3D Demo
File: `examples\04_bangrender_3d.bang`

```bang
import bangrender3d;

fn main() -> void {
    bangrender3d.demo();
}

main();
```

### 5.2 Planned 3D API (next steps)
- `render3d.init(w,h,title)`
- `render3d.camera.set(px,py,pz, tx,ty,tz)`
- `render3d.mesh.load("model.obj")`
- `render3d.mesh.draw(id)`
- `render3d.present()`

## 6) WebBang (WASM)

**WebBang** is the built?in web library (WASM). It renders to DOM and Canvas.

### 6.1 WebBang Example
File: `examples\05_webbang.bang`

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

### 6.2 Build and Run Web

```powershell
# build + run local server
bang web run
```

Open in browser:
```
http://localhost:8000
```

## 7) Examples Summary

- `01_language.bang` — base language syntax
- `02_program.bang` — small utility program
- `03_bangrender_2d.bang` — 2D game loop with BangRender
- `04_bangrender_3d.bang` — 3D demo (rotating cube)
- `05_webbang.bang` — WebBang (WASM) demo

## 8) Performance Notes

- Use `bangrender.fps(60)` or lower to reduce CPU usage.
- Keep loops tight and avoid heavy work in `while` without limits.
- For WebBang, performance depends on browser and device.

## 9) Roadmap (Short)

- Structured 3D API (camera/mesh/material)
- OBJ loader
- WebBang UI widgets (buttons, inputs)
- Package system for third?party libs

---

Bang is built to be fast, simple, and fun. If you want changes or new features, update this doc and the language will follow.
