Some additional tools to be use with pydantic 

In development 

# Installation 

```shell
> git clone https://github.com/efisoft-elt/pydantic_tool
> cd pydantic_tool 
> python setup.py install
```

# RecDefault

Recusrsive default for sub-model. This is used for instance when the payload is inclonplete but one wants to define some
default values per sub-model instances: 

```python 
from pydantic_tool import RecDefault
from pydantic import BaseModel 

class Value(BaseModel):
    name: str = ""
    unit: str = ""
    
    data: float = 0.0

class Experiment(BaseModel):
    
    length: RecDefault[Value] = Value(name="length of th stuff", unit="mm")
    time:   RecDefault[Value] = Value(name="time", unit="s")

 
e = Experiment( length = {'data': 0.56} ) 
assert e.length.unit == 'mm' # Without the RecDefault unit would be ""

```
