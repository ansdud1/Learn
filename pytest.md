> [pytest documentation](https://docs.pytest.org/en/latest/reference/reference.html)
> Reference : Python Testing with pytest by Brian Okken

# Naming Convention

* Test files should be named `test_<something>.py` (or `<something>_test.py`).  

* Test methods and functions should be named `test_<something>`.

* Test classes should be named `Test<Something>`.

# Test function structure

* Given/Arrange—A starting state. This is where you set up data or the environment to get ready for the action.

* When/Act—Some action is performed. This is the focus of the test—the behavior we are trying to make sure is working right.

* Then/Assert—Some expected result or end state should happen. At the end of the test, we make sure the action resulted in the expected behavior.

# Using assert statements

* `assert something`
* `assert not something`
* `assert a == b`
* `assert a != b`
* `assert a is None`
* `assert a is not None`
* `assert a <= b`

# handle exception expected. 
```python
def test_exception_raise
    expect = "{exception message}"
    
    with pytest.raises({Type of Exception}) as ex_info:
        code which raise exception.
    
    assert expected in str(ex_info.value)


    expect_regex = "{regular expression}"
    with pytest.raises({Type of Exception}, match=expect_regex) :
        code which raise exception.
    

```


# Test run 

* pytest: With no arguments, pytest searches the local directory and subdirectories for tests.

* pytest <filename>: Runs the tests in one file

* pytest <filename> <filename> ...: Runs the tests in multiple named files

* pytest <dirname>: Starts in a particular directory (or more than one) and recursively searches for tests

## run subset of tests

| Subset                        | Syntax                                                      |
|-------------------------------|-------------------------------------------------------------|
| Single test method            | `pytest path/test_module.py::TestClass::test_method`        |
| All tests in a class          | `pytest path/test_module.py::TestClass`                     |
| Single test function          | `pytest path/test_module.py::test_function`                 |
| All tests in a module         | `pytest path/test_module.py`                                |
| All tests in a directory      | `pytest path`                                               |
| Tests matching a name pattern | `pytest -k pattern`                                         |
| Tests by marker               | *Markers*.                                                  |

> **Note:** Use `--tb=no` to turn off tracebacks.

> name pattern can be multiple conditions with 'or' and 'and' , "{pattern to include } and not {pattern}"

# Test output

* PASED (.)—The test ran successfully.

* FAILED (F)—The test did not run successfully.

* SKIPPED (s)—The test was skipped. You can tell pytest to skip a test by using either the @pytest.mark.skip() or @pytest.mark.skipif() decorators

* XFAIL (x)—The test was not supposed to pass, and it ran and failed. You can tell pytest that a test is expected to fail by using the @pytest.mark.xfail() decorator​.

* XPASS (X)—The test was marked with xfail, but it ran and passed.

* ERROR (E)—An exception happened either during the execution of a fixture or hook function, and not during the execution of a test function. 


# Fixtures

Fixtures are functions that are run by pytest before (and sometimes after) the actual test functions.
used to get data ready for multiple tests.

decorator : @pytest.fixture()
include the fixture name in the parameter list of the test function. 

```  python 
@pytest.fixture()
def some_data():
    """Return answer to ultimate question."""
    return 42
def test_some_data(some_data):
    """Use fixture return value in a test."""
    assert some_data == 42
```
