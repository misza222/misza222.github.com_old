---
layout: post
title:  "Iterative deepening and with reliable timeout"
date:   2017-05-10 09:00:00 -0100
categories: ai
---

Use case for [iterative deepening](https://en.wikipedia.org/wiki/Iterative_deepening_depth-first_search) is to return most complete result it is possible within a certain time constraint.

Here is my implementation of the timer and how to handle it in Python. It is Unix specific as it uses BSD signals, and will not work on Windows (but works on Mac of course).

{% highlight python %}
import signal
import time

class TimeOut():
    """
        TimeOut for *nix systems
    """
    class TimeOutException(Exception):
        pass

    def __init__(self, sec):
        self.sec = sec # time we want an exception to be raised after
        self.start_time = None # to measure actual time

    def start(self):
        self.start_time = time.time()
        signal.signal(signal.SIGALRM, self.raise_timeout)
        signal.alarm(self.sec)

    def raise_timeout(self, *args):
        signal.alarm(0) # disable
        message = "Alarm set for {}s and actually passed {}s".format(self.sec,  round(time.time() - self.start_time, 5))
        raise TimeOut.TimeOutException(message)


def fibonacci(n):
  """
    This is used to simulate a depth first search
  """
    if n < 2:
        return n
    return fibonacci(n-2) + fibonacci(n-1)

def iterative_deepening(timeout):
    result = None # we store best result here
    depth = 1 # depth of the current search
    try:
        TimeOut(timeout).start()
        while True:
            result = fibonacci(depth)
            depth += 1

    except TimeOut.TimeOutException as e:
        print(e) # If we are not bothered by nanosecond differences, this is good enough

    return result, depth

if __name__ == '__main__':
    for timeout in range(1,10):
        result, depth = iterative_deepening(timeout)
        print ("After ", timeout, " seconds reached depth is ", depth, " with a result ", result)
{% endhighlight %}
