# Citadel-Build-the-algorithmic-Black-Box - 24B3019
 

## WEEK 0 — Core Concepts & Setup

This week was about understanding how a Limit Order Book works and setting up the basic skeleton of the project.

###  Goals

- Understand bids, asks, price levels, FIFO ordering
- Learn matching rule:  
Trade happens if best_bid >= best_ask

- Decide to use a **discrete event clock**, not wall-clock time
- Create the basic project structure

###  Initial Project Layout
.
├── market.py # Order + OrderBook classes
├── simulator.py # Clock + engine shell
└── main.py # testing & running

###  Key Takeaways

- **Bids are sorted descending**
- **Asks are sorted ascending**
- Orders at the same price follow FIFO  
- Deterministic replay is CRUCIAL for debugging

No fancy stuff yet — just strong fundamentals.

---

##  WEEK 1 — Matching Engine & Order Book Logic

This is where the real engine was built.

###  Goals

- Implement:
  - limit orders
  - market orders
  - FIFO inside price levels
- Maintain **sorted bid/ask books**
- Execute trades when:

- 
### 🔧 Features Added

- Insert orders into correct price levels
- Partial fills supported
- Auto-remove empty price levels
- Deterministic timestamps per event
- Trade log created

###  Example Logic (Conceptual)



Receive order

If it crosses the spread → match

Fill as much as possible

If quantity remains → store in book

markdown
Copy code

###  Result

We now have a **fully-functioning LOB matching engine**.

---

##  WEEK 2 — Agents, Simulation Loop & Depth View

Now we move from “engine” → “market simulator”.

###  Goals

- Add **Agent interface**
- Build a **Simulator that runs event-by-event**
- Add utilities to print **top-of-book + depth**
- Make everything replay-deterministic

###  Agent System

Agents can:

- submit limit orders
- submit market orders
- cancel orders
- read state from the book

A simple **RandomAgent** was added for testing — you can later replace it with smarter RL/alpha-based logic.

###  Discrete Event Simulator

The simulator handles:

- advancing time
- routing orders to the book
- printing state
- verifying same stream → same trades

###  Order Book Depth Output

Example output looks like:

Time = 12

BIDS
101.20 x 300
101.00 x 150

ASKS
101.50 x 200
101.80 x 250


###  Final Structure



.
├── market.py # Order book + matching
├── agents.py # Base + RandomAgent
├── simulator.py # Discrete event simulator
└── main.py # Run example

---

##  Future Ideas

Some natural next steps:

- add latency
- add PnL tracking
- multiple agents interacting
- plot depth charts
- RL training loop
- order expiry

---

##  Requirements

Python **3.9+**

No external libs required unless you add plotting later.

---

##  Running the Simulator


python main.py


best_bid >= best_ask
best_bid >= best_askbest_bid >= best_ask
