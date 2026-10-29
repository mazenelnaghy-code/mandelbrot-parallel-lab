# Mandelbrot Parallel Lab

An interactive one-page lab that shows when parallel code is faster, and when it is slower. It draws the
Mandelbrot fractal with real parallel workers in your browser, and backs every claim with timings measured
in Python.

Course project for **CCE 424 Parallel Processing**.

## Results

Measured with Python's `multiprocessing` on an Intel i7-8550U laptop (4 cores / 8 threads):

| Version | Time | Compared with sequential |
|---|---|---|
| Sequential, 1 core | 3.60 s | baseline |
| Parallel, 4 processes, rows as tasks | 1.48 s | **2.4× faster** |
| Parallel, one task per pixel | 29.23 s | about 8× slower |

- **Overhead:** sending one pixel per task means thousands of messages, and delivering them costs more than the work itself.
- **Load balancing:** the middle of the fractal is harder to draw. Four big strips leave two cores idle (2.03 s); many small chunks keep every core busy (1.53 s).

## What's inside

- **Live demo:** draws the fractal in your browser with Web Workers. Choose 1, 2, 4 or 8 workers and the task size, and colour each core's part to see who drew what.
- **Why Mandelbrot:** five candidate projects tested and compared on speed-up, overhead and load balancing.
- **Measured results:** sequential vs parallel vs threads, speed-up per number of processes, overhead and load balancing.
- **How the work is split,** what overhead is and how to fix it, and why 4 cores never give a 4× speed-up.
- **The code:** all three versions in about 40 lines of Python, ready to copy and run.

## Run it

Open `index.html` in any modern browser. It is a single file with no build step.

To reproduce the Python timings, copy the code from the page into `mandel.py` and run:

```bash
python mandel.py
```

## Built with

HTML · CSS · JavaScript (Web Workers) · Python `multiprocessing`

See also [parallel-python-projects](https://github.com/mazenelnaghy-code/parallel-python-projects), the comparison of
nine project ideas that led to this one.

Built by [Mazen Elnaghy](https://github.com/mazenelnaghy-code).
