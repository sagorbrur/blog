---
title: Python Argparse এ হাতে খড়ি
---




মেশিন লার্নিং জগতে কিংবা পাইথন এডভান্স প্রোগ্রামিং এ আর্গুমেন্ট পার্সিং একটি মহা প্রয়োজনীয় কাজ। 
মূলত এটিকে `Command Line Argument` ও বলা হয়ে থাকে। `Command Line Argument` হলো কিছু ভ্যারিয়েবল টাইপ আর্গুমেন্ট যেগুলো কোন প্রোগ্রামিং স্ক্রিপ্ট রান টাইমে প্রদান করা হয়। 


যেমনঃ `python test.py --value1 2 --value2 3`

এখানে `--value1 2` `--value2 3` হলো `Command Line Argument` যা `test.py` প্রোগ্রামিং স্ক্রিপ্ট রান করানোর সময় প্রদান করা হলো। 

## কেন `Command Line Argument` দরকার

* **এটি প্রোগ্রাম স্ক্রিপ্টকে বিভিন্ন আলাদা ইনপুট প্রদান করে স্ক্রিপ্টের কোন পরিবর্তন ছাড়াই।**
* **ডিপ লার্নিং এ `model_path`, `data_path`, `epoch` সচরাচর পরিবর্তন করতে হয়। `Command Line Argument` তাই এখানে একটি অতি গুরুবপূর্ণ সযোগিতা করে।**

## পাইথনে `Command Line Argument` 

পাইথন স্টান্ডার্ড লাইব্রেরির অন্তর্গত `Argparse` মডিউল `Command Line Argument` সুবিধা প্রদান করে থাকে।

## উদাহরণ ও রান প্রক্রিয়া

```py
import argparse

# construct the argument parse
arg = argparse.ArgumentParser()

# add argument
arg.add_argument("-v1", "--value1", required=True,
   help="first value")
arg.add_argument("-v2", "--value2", required=True,
   help="second value")
args = vars(arg.parse_args())

# Calculate the sum
print("Sum is {}".format(int(args['value1']) + int(args['value2'])))

```


* এখানে `-v1` ও `-v2` হলো `shorthand`  আর্গুমেন্ট এবং `--value1` ও `--value2` হলো `longhand` আর্গুমেন্ট। আমরা দুটির যেকোন একটিকে আর্গুমেন্ট হিসেবে পাস করাতে পারবো। 
* আর্গুমেন্টটি বাধ্যতামুলক নাকি ঐচ্ছিক তা `required` ফিল্ড দিয়ে প্রদান করা হয়। 
* `help` আর্গুমেন্টটি সম্পর্কে অতিরিক্ত তথ্য প্রদান করে। 

### ইক্সেকিউশন প্রণালী
* প্রথমে স্ক্রিপ্টটি `arg_test.py` নামে সেভ করুণ। 
* টার্মিনাল ওপেন করে নিচের কম্যান্ডটি লিখুন। 

`python arg_test.py --value1 2 --value2 3`

output: Sum is 5


## আরো কিছু উদাহরণ

* **ডিফল্ট আর্গুমেন্ট**

```py
import argparse

# construct the argument parse
arg = argparse.ArgumentParser()

# add argument
arg.add_argument("-n", "--name", default='Sagor',
   help="Enter your name")
args = vars(arg.parse_args())

# Calculate the sum
print('Your name is {}'.format(args['name']))
```

**compile**

`test.py` নামে সেভ করুণ আর নিচের command টি রান করুণ। 

`python test.py` 

output: Your name is Sagor

`python test.py --n Ripon`

output: Your name is Ripon


* **আর্গুমেন্ট টাইপ**

```py
import argparse

# construct the argument parse
arg = argparse.ArgumentParser()

# add argument
arg.add_argument("-n", "--value", type=int,
   help="Enter int value")
args = vars(arg.parse_args())

# Calculate the sum
print('The value is {}'.format(args['value']))
print('value type is: ', type(args['value']))
```

**compile**

`test2.py` নামে সেভ করুণ আর নিচের command টি রান করুণ। 

`python test2.py` --value 2

output: The value is 2

value type is <class, 'int'>

## References

1. [https://docs.python.org/3/library/argparse.html](https://docs.python.org/3/library/argparse.html)
2. [https://www.pyimagesearch.com/2018/03/12/python-argparse-command-line-arguments/](https://www.pyimagesearch.com/2018/03/12/python-argparse-command-line-arguments/)
