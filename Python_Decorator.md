# Python Decorator
```
import time


def debug_time(function_to_call):
    def inner_function(*args, **kwargs):
        print('---DEBUG START TIME FOR {0}'.format(function_to_call))
        start_time = time.clock()
        value = function_to_call(*args, **kwargs)
        end_time = time.clock()
        print('---DEBUG END TIME')
        print("---DEBUG TOOK {0:.4f} SEC.".format(end_time - start_time))
        return value

    return inner_function


@debug_time
def debugtest(sleep_how_long):
    time.sleep(sleep_how_long)


@debug_time
def debugtest2(what_to_print):
    time.sleep(1.5)
    print(what_to_print)


debugtest(2)
debugtest2('NEW TEST')
```
