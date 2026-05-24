# MacNode 

execution layer for spawning, managing, and evolving token-protected threads
CPU or Apple GPU (Metal) — controlled, fast, precise

not just tasks → **nodes of execution**

---

## ⚡ FEATURES

* **Thread Runtime** — define + execute nodes with priority, sandboxing, caching
* **Secure Tokens** — per-node validation
* **CPU Engine** — Numba-powered parallel execution
* **GPU Path** — Swift/Metal bridge (`libMetalBridge.dylib`)
* **Persistent Registry** — JSON-backed (`thread_registry.json`)
* **Node History** — full timeline tracking
* **Batch Spawn** — launch multiple nodes instantly
* **Advanced Ops** — branch • fork • merge • reparent • rename • mutate

---

## 🧠 CORE IDEA

> nodes = controlled execution units
> created • tracked • modified • evolved

---

## 🧩 STRUCTURE

FAHH-Node/
├─ core/
│  ├─ create.py        → node runtime (CPU/GPU)
│  ├─ operations.py    → registry ops
│  ├─ delete.py        → CLI (delete + archive)
│  ├─ router.py        → future orchestration
│  └─ swift/
│     ├─ GPU.swift
│     ├─ MetalBridge.swift
│     └─ libMetalBridge.dylib
├─ main.py
├─ requirements.txt
└─ thread_registry.json

---

## ⚙️ REQUIREMENTS

* Python 3.9+
* macOS + Metal (for GPU path)

deps:

* psutil
* numba
* numpy

install:
pip install -r requirements.txt

---

## 🚀 QUICK START

generate token + create node:

from core.create import CreateThread, generate_token

token = generate_token()

node = CreateThread(
thread_id=1.0,
stage="CORE",
device="cpu",
token=token,
caching=True,
priority=2,
ttl=15.0,
metadata={"max_memory_mb": 1000},
thread_name="CoreNode",
)

node.spawn(dry_run=False)

---

## 🔍 REGISTRY

* storage → `thread_registry.json`
* deleted backup → `deleted_threads.json`

query:

from core.operations import list_threads, get_thread

list_threads()
get_thread(1.0)

---

## ⚡ EXECUTION MODES

**CPU**

* Numba-parallel kernels
* stable + portable

**GPU (Metal)**

* Swift bridge → `run_gpu_thread`
* requires compiled dylib

---

## 🧪 CLI

delete + archive nodes:

python -m core.delete 1.0 2.0

---

## ⚠️ NOTES

* ensure `libMetalBridge.dylib` path is correct
* run from correct directory or adjust loader path
* corrupted registry auto-recovers (with warning)

---

* IDK why i created this.
* USe at you own risk, it may or may not work or deep fry your mac or VM.
* Readme by ai cuz im lazy , and code by my glitched mind. 
