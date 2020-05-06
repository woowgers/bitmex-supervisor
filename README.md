# BitMEX Supervisor

This is a library-like application, which operates with orders and positions on your account.

**Current version: 0.1, in development**
#### Features:
* Creating an cancelling orders on your account. Stop-loss, Limit, passive, reduce-only, close-only, hidden orders supported.
* Preventing these orders for being lost, cancelled or rejected: Supervisor will place them anew.
* Supervisor closes all orders, which are not supervised.
* When the supervised order has been filled, Supervisor will not try to place it. 
#### In develop:
* Manage positions on your account.
    * Maintaining position size.
    * Various market-price or limit entries in position.
    * Enter position with rebate by tracking last market price and moving limit order up.
* Put callbacks on supervised orders, which are called when order has been filled, partially executed or cancelled.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

For now we support only the version of Python that we use in development.

```
Pyhton 3.8 +
```

### Installing

#### Manual install from repo

Clone and go to directory:

```commandline
git clone https://github.com/forkcs/bitmex-supervisor.git
cd bitmex-supervisor/
```

Then create and activate a virtual environment:

```commandline
python3 -m venv venv
source venv/bin/activate
```

Install project requirements:

```commandline
pip install -r requirements.txt
```

#### Install with pip

Coming soon...

#### Install from sources

Coming soon...

#### After successful installation:

Now you can import supervisor module from project dir:
```python
import supervisor
```
For more details see example.py.

### Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Usage

Create Exchange instance:

```python
from supervisor.core.interface import Exchange

exchange = Exchange(symbol='XBTUSD',
                    api_key='YOUR_API_KEY',
                    api_secret='YOUR_API_SECRET',
                    test=True)       # test=True for use Testnet
```

Create Supervisor instance:

```python
from supervisor import Supervisor

supervisor = Supervisor(interface=exchange)
```

Create order:

```python
from decimal import Decimal
from supervisor.core.orders import Order

my_order = Order(order_type='Limit', qty=100, side='Buy', price=Decimal(6500), hidden=True, passive=True)

supervisor.add_order(my_order)
```

Run Supervisor cycle (wors in own thread):

```python
supervisor.run_cycle()
```

You also can stop, continue and exit Supervisor cycle:

```python
supervisor.stop_cycle()
# do staff
supervisor.run_cycle()  # this method can both run and continue cycle
supervisor.exit_cycle() # this method terminates cycle`s thread and quit correctly
```

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Fedor Soldatkin** - *Initial work* - [forkcs](https://github.com/forkcs)


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE) file for details.

