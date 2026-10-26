# Honors Quantum Computing & ML – Qiskit Codespace

Everything you need for the Qiskit problem sets runs **in your browser**. Nothing to install on your laptop, and everyone gets exactly the same setup (Python 3.12, Qiskit 2.6, Qiskit Aer simulator).

You need a free personal **GitHub account** (sign up at <https://github.com/signup>, age 13+).

---

## 1. Open your codespace (first time)

1. Sign in to GitHub and open this repository page.
2. Click the green **Use this template** button → **Open in a codespace**.
   - *(Alternative: **Code** → **Codespaces** tab → **Create codespace on main**.)*
3. Wait about 1–2 minutes the first time while it sets up. When the terminal says
   `Qiskit 2.6.0 | Aer 0.18.0 - ready`, you're good.
4. Open `notebooks/00_check_setup.ipynb` and click **Run All** (▶▶).
   - If asked to **Select Kernel**, choose **Python Environments → Python 3.12 (/usr/local/bin/python)**.
   - You should see a circuit drawing, a histogram with only `00` and `11`, and a ✅ at the bottom.

**Next time:** go to <https://github.com/codespaces> and click your existing codespace to reopen it. Don't create a new one each time, because your files live inside the one you already have.

## 2. Do a problem set

- Open the notebook for the problem set (for example `notebooks/PS4_template.ipynb`). To keep the blank version, right-click it → **Copy**, then **Paste** and rename it (e.g. `PS4_Firstname.ipynb`).
- Put your name in the first cell.
- Write your **predictions by hand first** in the markdown cells, then run the code, then explain.
- It's fine to use AI for code, but old Qiskit code from AI often breaks. The notebooks have a table of outdated commands (`execute`, `Aer`, `IBMQ`, …) and what to use instead.

## 3. Submit on Canvas

1. **Restart** the kernel and **Run All** so every output shows, then save with `Ctrl+S` / `Cmd+S`.
2. In the file Explorer on the left, **right-click your notebook → Download…**
3. Upload the downloaded `.ipynb` to the Canvas assignment.

> Your codespace is **not** a backup. A stopped codespace is deleted automatically after 30 days without use. Always download your finished `.ipynb` and submit it to Canvas.

## 4. Stop the codespace when you're done (saves your free hours)

Closing the browser tab does **not** stop it right away; it keeps running until it has been idle for 30 minutes.

- Click the green/blue **Codespaces** button at the bottom-left → **Stop Current Codespace**, **or**
- go to <https://github.com/codespaces> → `…` next to your codespace → **Stop codespace**.

Your saved files are kept when it's stopped.

## 5. Free-tier notes

A free GitHub account includes **120 core-hours** and **15 GB-month storage** per month. This codespace uses a 2-core machine, so that's about **60 hours of running time a month**, far more than the problem sets need. Storage for one codespace is roughly 3 GB.

- Keep **one** codespace for this class, and delete any extras at <https://github.com/codespaces>.
- Don't change the machine type to 4-core or bigger. It burns hours 2× or more faster.
- If you hit the limit, GitHub simply blocks new usage until the next month. It never charges you unless you add a payment method yourself. **Don't add one.**

## Troubleshooting

| Problem | Fix |
|---|---|
| "Select Kernel" keeps popping up | Pick **Python 3.12 (/usr/local/bin/python)**. |
| `ModuleNotFoundError: qiskit` | Wrong kernel. See above, or in the terminal run `pip install -r requirements.txt`. |
| `ImportError: cannot import name 'execute'` (or `Aer`, `IBMQ`) | That's outdated code. Use the table in the notebook. |
| Histogram shows `01` when you expected `10` | Qiskit puts **qubit 0 on the right** of the bitstring. |
| Codespace won't start / "usage limit" | Tell Mr. Bayntun. Download your notebook first if you can. |
