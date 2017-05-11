First try for a python wrapper around JMad. Needs cmmnbuild-dep-manager (and access to CERN resources) to run.

Set up:
```python
import pyjmad
jmad = pyjmad.JMad()
```

Get all model definitions:
```python
jmad.model_definitions
```

Create a Model:
```python
md = jmad.model_definitions['LHC 2017']
jmad.create_model(md)
```
or simply:
```python
lhcModel = jmad.create_model('LHC 2017')
```

Set a Sequence and Optic to use:
```python
lhcModel.sequence = 'lhcb1'
lhcModel.optic = 'R2017a_A11mC11mA10mL10m'
```

Twiss it:
```python
twiss = lhcModel.twiss(variables=('S','BETX','BETY','X','Y'))
```
This will return a namedtuple:
* ``twiss.summary`` is a dict of the twiss summary
* ``twiss.data`` is a Pandas DataFrame of the twiss results

Plot it:
```python
plt.figure()
plt.plot(res.data.S, res.data.BETX)
plt.plot(res.data.S, res.data.BETY)
plt.show()
```

Open a JMad GUI (sharing the state with the python script) for interactive exploration:
```python
jmad.open_jmad_gui()
```