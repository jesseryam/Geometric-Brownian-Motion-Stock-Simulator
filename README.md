# Geometric-Brownian-Motion-Stock-Simulator
A Monte Carlo stock price simulator built in Processing, implementing the same mathematical model that shows the Black-Scholes options pricing formula

Geometric Brownian Motion Stock Simulator

I built this project to get a hands-on understanding of how stock prices are mathematically modeled in quantitative finance. It implements Geometric Brownian Motion — the same model that underlies Black-Scholes, which won the Nobel Prize in Economics in 1997 and still sits at the foundation of how options are priced on every trading desk in the world.

The idea behind GBM

Stock prices move for two reasons — there's the slow predictable drift upward that reflects the market's long run expected return, and then there's the daily randomness that nobody can predict. GBM captures both:

P(t+1) = P(t) * e^( (mu - 0.5 * sigma²) * dt + sigma * sqrt(dt) * Z )

The mu term handles the drift, set to 7% annually to reflect historical S&P 500 returns. The sigma term handles volatility, set to 20% which is roughly what the broader market averages. Z is a random number drawn from a normal distribution every single day — it's what makes each simulation different from the last.

One thing I found interesting while building this: the reason we use e instead of just multiplying prices directly is that e guarantees the stock price can never go negative. Even if Z produces a catastrophic number, e raised to any power stays positive. That's a mathematical requirement that reflects how stocks actually behave in reality.

What it does

Starting from $100 the simulator runs a stock through 252 trading days — one full year. Press a key and you get one path. Click the mouse and it runs 10,000 simulations and tells you the average final price and the probability of ending above $120. Watching 10,000 paths pile up on the canvas makes the probability distribution tangible in a way that just reading about it never did for me.

Where the model breaks down

GBM is a starting point not a complete picture, and it has some well known flaws worth being honest about.
The biggest one is fat tails. The normal distribution that Z is drawn from says a five sigma crash should happen once every few billion years. In reality markets see events like that every decade or so — 2008, March 2020, the 1987 flash crash. GBM systematically underestimates how often extreme things happen.

Volatility is also assumed to be constant at 20% which is never true in practice. Real volatility spikes during crises and compresses during calm periods. The Heston model addresses this by making sigma itself a random variable, which is something I want to implement next.
