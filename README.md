Fanova
======

Functional ANOVA: an implementation of the ICML 2014 paper "An Efficient Approach for Assessing Hyperparameter Importance" by Frank Hutter, Holger Hoos and Kevin Leyton-Brown.

Requirements
------------


Installation
------------

### Pip


```
pip install fanova
```


### Manually

```
python setup.py install
```
 
Example usage
-------------

To run the examples, just start Python console.
We can then import Fanova and start it by typing
```python
>>> from fanova import Fanova
>>> f = Fanova("example/online_lda")
```
This creates a new Fanova object and fits the Random Forest on the specified data set. To compute now the marginal of the first parameter type:
```python
>>> f.get_marginal(0)
5.44551614362
```
Fanova also allows to specify parameters by their names.
```python
>>> f.get_marginal("Col0")
5.44551614362
```
Pairwise marginals of two parameters can be computed with the command
```python
>>>  f.get_pairwise_marginal(0, 1)
0.9370525790628655
```
Again the same can been done by specifing names instead of indices
```python
>>> f.get_pairwise_marginal("Col0","Col1")
0.9370525790628655
```
If we want to compute the mean and standard deviation of a parameter for a certain value, we can use
```python
>>> f.get_marginal_for_value("Col0", 0.1)
(1956.6644432031385, 110.58740682895211)
```
To visualize the single and pairwise marginals, we have to create a visualizer object first
```python
>>> from visualizer import Visualizer
>>> vis = Visualizer(f)
```
We can then plot single marginals by 
```python
>>> plot = vis.plot_marginal(1)
>>> plot.show()
```
The same can been than for pairwise marginals
```python
>>> vis.plot_pairwise_marginal(0, 2)
```
At last, all plots can be created together and stored in a directory with
```python
>>> vis.create_all_plots("./plots/")
```

If your data is stored in csv file, you can run Fanova with
```python
>>> from fanova_from_csv import FanovaFromCSV
>>> f = FanovaFromCSV("/path_to_data/data.csv")
```
It is also possible to run Fanova on data colleted by [HPOlib](http://www.automl.org/hpolib)
```python
>>> from fanova_from_hpolib import FanovaFromHPOLib
>>> f = FanovaFromHPOLib("/path_to_hpolib_data/")
```
