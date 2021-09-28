# Summary

## Defintions

Iterables: lists, dictionaries, sets, tuples, strings, files.

An iterable is an object that you can get an iterator from. An iterable is an object that has an __iter__ method which returns an iterator, or which defines a __getitem__ method that can take sequential indexes starting from zero (and raises an IndexError when the indexes are no longer valid). 
An iterator is an object with a next (Python 2) or __next__ (Python 3) method. ([REF])(https://stackoverflow.com/questions/9884132/what-exactly-are-iterator-iterable-and-iteration)

Every generator is an iterator, but not vice versa. A generator is built by calling a function that has one or more yield expressions.

Making a function a generator makes them general purpose. (for lists, dicts, sets, ...)

Generators: It is another way of creating iterators in a simple way where it uses the keyword “yield” instead of returning it in a defined function.  Generators are implemented using a function. 

Iterator vs.	Generator

Class is used to implement an iterator vs. Function is used to implement a generator.

Local Variables aren’t used here.  vs. All the local variables before the yield function are stored. 

Iterators are used mostly to iterate or convert other objects to an iterator using iter() function.   vs.  	Generators are mostly used in loops to generate an iterator by returning all the values in the loop without affecting the iteration of the loop

Iterator uses iter() and next() functions vs.	Generator uses yield keyword

Every iterator is not a generator vs. Every generator is an iterator ([REF])(https://www.geeksforgeeks.org/difference-between-iterator-vs-generator/)

Iterables:

List 	Simple Collection of Elements 	

    Has a consistent order
    Finding may require inspecting all elements

Set 	Unique collection of elements 	

    Has random order
    Finding items will be fast

Tuple 	Immutable collection of elements 	

    All elements in collection must be present at creation
    Immutability is useful to protect data from unintended changes

Dictionary 	Collections indexed by keys

    Can encode simple object-like data structures 	
    Has random order
    Lookup by key will be fast
    Simple data structures behave like temporary in-memory databases

([REF])(https://kkiesling.github.io/python-novice-gapminder-custom/05c-iterable-data-types/)

A callable object, in computer programming, is any object that can be called like a function. 

Python functions can contain two types of arguments: positional arguments and keyword arguments. Positional arguments must be included in the correct order. Keyword arguments are included with a keyword and equals sign.

An argument is a variable, value or object passed to a function or method as input. Positional arguments are arguments that need to be included in the proper position or order.

function(keyword=value)

complex(real=3, imag=5)

keyword_dict = {'real': 3, 'imag': 5}
complex(**keyword_dict)

vs.

complex(3, 5)

function(iterable)

term_list = [3, 5]
complex(*term_list)

## 1.1  Unpacking a sequence into separate variables: var1, var2, var3 = (1, 2, 3)

data = ['car', 5, 90.4, (2021,8,13)]
name, age, price, date = data

s = 'Hello'
a, b, c, d, e  = s

_, age, price, _ = data
print(age, price)

## 1.2 Unpacking elements from iterables of arbitrary length: first, *var, before_last, last = record

// The star *args syntax lets you fill in arguments from an iterable.

record = ('Rick', 'rick@no-reply.com', '798-415-215', '155-255-856')
name, email, *phone_numbers = record

line = 'hello:bla:234:blabla:2899:blablabla:important:more_important'
word, *fields, _, last = line.split(':')

## 1.3 Keeping the last N items: deque (Use deque instead of lists)

q = deque(maxlen=3)
q.appendleft(4)
q.popleft()
q.append(5)
q.pop()

## 1.4 Finding the largest or smallest N items: heapq

nums = [6, 1, 4, 5, 3, 45, 35, 23, 6786, 23, 4, 86, 57 ,34, 24]
print(heapq.nlargest(3, nums))
print(heapq.nsmallest(3, nums))

heapq.heapify(nums)
heapq.heappop(heap)

portfolio = [ {'price':85, ...}, {...}, ... ] 
cheap = heapq.nsmallest(3, portfolio, key=lambda s: s['price'])

## 1.5 Implementing a priority queue: heapq.push and heapq.pop

heapq.heappush(list, (-priority, index, item))
heapq.heappop(self._queue)

one can perform < operations with heaps

## 1.6 Mapping keys to multiple values in a dictionary: defaultdict

d = defaultdict(list)
d['a'].append(1)

e = defaultdict(set)
e['a'].add(1)

// The problem with defaultdict is that it will create dict entries for keys accessed later on 
// (even if they are not found in the dict).

d = {} # regular dict
d.setdefault('a', []).append(1)

## 1.7 Keeping dictionaries in order: OrderedDict

// preserving the order of the input items
d = OrderedDict()
d['foo'] = 1
json.dumps(d)

## 1.8  Calculating with dictionaries: max(zip(values,keys)

prices = { 'name':95, ...}
min_price = min(zip(prices.values(), prices.keys()))
// However, zip creates an iterator that can only be used once
min_key = min(prices, key=lambda k: prices[k])
min_value = prices[min(prices, key=lambda k: prices[k])]

## 1.9 Finding commonalities in two dictionaries: .keys(), .items() set operations

// finding commonalities between two dictionaries
// between sets
// Keys in common
a.keys() & b.keys()
// keys in a that are not in b
a.keys() - b.keys()
// find (key,value) pairs in common
a.items() & b.items()

## 1.10 Removing duplicates from a sequence while maintaining order

def dedupe(items, key=None):
    seen = set()
    for item in items:
        # the anonymous function (lambda) will yield a tuple, which is hashable
        val = item if key is None else key(item) 
        if val not in seen:
            yield item
            seen.add(val)

a = [{'x':1, 'y':2}, {'x':1, 'y':3}, {'x':1, 'y':2}, {'x':2, 'y':4}]
print(list(dedupe(a, key=lambda d: (d['x'], d['y']))))

## 1.11 Naming a slice

record = '4156418964165484684649595846848487879'
SHARES = slice(5,10)
PRICE = slice(15,20)
cost = int(record[SHARES]) * float(record[PRICE])
cost

## 1.12 Determining the most frequent ocurring items in a sequence

from collections import Counter

words = [
    'look', 'into', 'my', 'eyes', 'look', 'look', 'look', 'eyes', 'eyes'
]

word_counts = Counter(words)
top_three = word_counts.most_common(3)

// you can also aply math operations on the words


## 1.13. Sorting a list of dictionaries by a common key

from operator import itemgetter

rows = [
    {'fname': 'Brian', 'lname': 'Jones', 'uid':1003},
    {'fname': 'David', 'lname': 'Beazley', 'uid':1002},
    {'fname': 'John', 'lname': 'Cleese', 'uid':1001}, 
    {'fname': 'Big', 'lname': 'Jones', 'uid':1004},    
]

rows_by_uid = sorted(rows, key=itemgetter('uid'))
rows_by_laname_fname = sorted(rows, key=itemgetter('lname', 'fname'))

## 1.14 Sorting objects without native comparison support

The built-in sorted() function takes a key argument that can be passed a callable that will return some value in the object that sorted will use to compare the objects.

class User:
    def __init__(self, user_id):
        self.user_id = user_id
    def __repr__(self):
        return 'User({!r})'.format(self.user_id)

users = [User(23), User(2), User(99)]
print(users)

sorted(users, key=lambda u: u.user_id)

// a tad faster

from operator import attrgetter

sorted(users, key=attrgetter('user_id'))

## 1.15 Grouping records together based on a field

// You have a sequene of dicts or instances and you want to iterate over the data in groups based on the value of a particular field, such as date.

// You can use iterable.sort(key=itemgetter('string')), which will overwrite the iterable
or new_iterable = sorted(iterable, key=...)

rows = [
    {'fname': 'Brian', 'lname': 'Jones', 'uid':1003},
    {'fname': 'David', 'lname': 'Beazley', 'uid':1002},
    {'fname': 'John', 'lname': 'Cleese', 'uid':1001}, 
    {'fname': 'Big', 'lname': 'Jones', 'uid':1004},    
    {'fname': 'Big', 'lname': 'Jones', 'uid':1004},
    {'fname': 'Big', 'lname': 'Jones', 'uid':1003},
    {'fname': 'Big', 'lname': 'Jones', 'uid':1002},
]

// sort by the desired field first. If you do nor sort, groupby will not group correctly
// as it only clusters adjacent equal values
rows.sort(key=itemgetter('uid'))
// same as: rows_by_fname = sorted(rows, key=itemgetter('uid'))

// iterate in groups
for uid, items in groupby(rows, key=itemgetter('uid')):
    print(uid)
    for i in items:
        print('    ', i)

## 1.16 Filtering sequence elements

// 1

// The output size might be a concern, to avoid that, you can use generators
pos = (n for n in mylist if n > 0)
pos

// to print
for x in pos:
    print(x)

// 2
values = ['1', '4', '-5', '10', '-', '-7', '2', '3', -1, 'N/A']

def is_int(val):
    try:
        x = int(val)
        return True
    except ValueError:
        return False
    
ivals = list(filter(is_int, values))
print(ivals)
type(ivals)

// filter creates an iterator, so use list to provide a list of results (iterable)

// 3

addresses = ['here', 'there', 'over there', 'further away', 'much further']
counts = [0, 4, 3, 5, 6]

from itertools import compress

more5 = [n>=5 for n in counts]
print(more5)
// remember to add list, as compress returns an iterable
list(compress(addresses, more5))

## 1.17 Extracting a subset of a dictionary

// dict comprehension

prices = {
    
    'ACME': 45.23,
    'APPL': 612.78,
    'IBM': 205.65,
    'HPQ': 37.5,
    'FB': 10.75
}

// Fastest options
p1 = {key:value for key, value in prices.items() if value > 200}

tech_names = {'APPL', 'IBM', 'HPQ', 'MSFT'}
p2 = {key:value for key, value in prices.items() if key in tech_names}

## 1.18 Mapping names to sequence elements: namedtuple and ._replace()

// You can access data by name and not position
Subscriber = namedtuple('Subscriber', ['addr', 'joined'])
sub = Subscriber(addr='myhome', joined='today')

// Tuples are immutable, but you can reinstantiate a new one with changes with

s = s._replace(shares=75)

## 1.19  Transforming and reducing data at the same time: generators

// The generator transforms data iteratively and it is more memeory efficient

s = sum(x*x for x in nums)

portfolio = [
    {'name':'frvw', 'shares':51},
    {'name':'wvgwrg', 'shares':514},
    {'name':'mtm', 'shares':75}
]

min_shares = min(s['shares'] for s in portfolio)

## 1.20 Combining multiple mappings into a single maping: chainmap

a = {'x':1, 'z':3}
b = {'y':2, 'z':4}

// For lookups. You first check in a and then in b if not found
c = ChainMap(a, b)



