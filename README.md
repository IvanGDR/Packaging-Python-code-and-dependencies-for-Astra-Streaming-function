# Packaging Python Code and Dependencies for Astra Streaming Function - (Python Zip file)

>Notes:
>For this task I am using a virtual environment but this may not need neccesary.
>
>The python version being used is 3.8.
>
>The .zip file to upload in Astra Sreaming, as of 5th Dec 2022, should not be more than 1GB weight or contain more than 5000 files. 




## Deployment package with no dependencies

#### 1) Go to your virtual environment, in my case:
```
$ conda activate eclipse
```
or
```
$ pyenv activate eclipse
```
after executing any of the above:
```
(eclipse) $
```

#### 2) Create a directory where yo will package your code and dependencies. I am creating this directory in my home directory:
```
(eclipse ) $ mkdir astra_streaming_function
```

#### 3) Navigate to the created directory:
```
(eclipse) $ cd astra_streaming_function
```
after:
```
(eclipse) astra_streaming_function $
```

#### 4) Copy/produce you working function code with the file name of your choice:

```
(eclipse) astra_streaming_function $ vi my_astra_function.py
```

The structure of the directory should be:

```
(eclipse) astra_streaming_function $ ls -la
```
```
-rw-rw-r-- ivan ivan  394 Dec  5 10:47 my_astra_function.py
```

#### 5) create a zip file, in this case my_package.zip and add the function my_astra_function.py to the root of the zip file

```
(eclipse) astra_streaming_function $ zip my_function_package.zip my_astra_function.py
```

The command produces the following output:
```
adding: my_astra_function.py (deflated 50%)
```

And the final result:
```
(eclipse) astra_streaming_function $ ls -la
```
```
-rw-rw-r-- ivang ivang      394 Dec  5 10:47 my_astra_function.py
-rw-rw-r-- ivang ivang 23509789 Dec  5 10:58 my_function_package.zip
```


## Deployment package with dependencies

#### 1) Go to your virtual environment, in my case:
```
$ conda activate eclipse
```
or
```
$ pyenv activate eclipse
```
after executing any of the above:
```
(eclipse) $
```

#### 2) Create a directory where you will package your code and dependencies. I am creating this directory in my home directory:
```
(eclipse ) $ mkdir astra_streaming_function
```

#### 3) Navigate to the created directory:
```
(eclipse) $ cd astra_streaming_function
```
after:
```
(eclipse) astra_streaming_function $
```

#### 4) Copy/produce you working function code with the file name of your choice:

```
(eclipse) astra_streaming_function $ vi my_astra_function.py
```

The structure of the directory should be:

```
(eclipse) astra_streaming_function $ ls -la
```
```
-rw-rw-r-- ivan ivan  394 Dec  5 10:47 my_astra_function.py
```

#### 5) Install the dependancies to a newly created "package" directory. For this example, I am installing two dependencies "numpy" and "datetime".

Note from where the following two commands are being executed, this is the working directory created in step  2.

Creating package directory and installing "numpy" dependancy
```
(eclipse) astra_streaming_function $ pip install --target ./package numpy
```

In package directory created already above, installing "datetime" dependancy
```
(eclipse) astra_streaming_function $ pip install --target ./package datetime
```
e.g. after executing the above
```
Collecting datetime
  Using cached DateTime-4.7-py2.py3-none-any.whl (52 kB)
Collecting zope.interface
  Using cached zope.interface-5.5.2-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (261 kB)
Collecting pytz
  Using cached pytz-2022.6-py2.py3-none-any.whl (498 kB)
Collecting setuptools
  Using cached setuptools-65.6.3-py3-none-any.whl (1.2 MB)
Installing collected packages: pytz, setuptools, zope.interface, datetime
Successfully installed datetime-4.7 pytz-2022.6 setuptools-65.6.3 zope.interface-5.5.2
```

The structure of the directory then:
```
(eclipse) astra_streaming_function $ ls -la
```
```
-rw-rw-r--  1 ivang ivang      394 Dec  5 10:47 my_astra_function.py
drwxrwxr-x 16 ivang ivang     4096 Dec  5 10:53 package
```
furthermore, listing content of "package" directory:
```
(eclipse) astra_streaming_function/package $ ls -la
```
```
drwxrwxr-x  2 ivang ivang 4096 Dec  5 10:52 bin
drwxrwxr-x  4 ivang ivang 4096 Dec  5 10:53 DateTime
drwxrwxr-x  2 ivang ivang 4096 Dec  5 10:53 DateTime-4.7.dist-info
drwxrwxr-x  3 ivang ivang 4096 Dec  5 10:52 _distutils_hack
-rw-rw-r--  1 ivang ivang  151 Dec  5 10:52 distutils-precedence.pth
drwxrwxr-x 21 ivang ivang 4096 Dec  5 10:52 numpy
drwxrwxr-x  2 ivang ivang 4096 Dec  5 10:52 numpy-1.23.5.dist-info
drwxrwxr-x  2 ivang ivang 4096 Dec  5 10:52 numpy.libs
drwxrwxr-x  5 ivang ivang 4096 Dec  5 10:52 pkg_resources
drwxrwxr-x  4 ivang ivang 4096 Dec  5 10:52 pytz
drwxrwxr-x  2 ivang ivang 4096 Dec  5 10:52 pytz-2022.6.dist-info
drwxrwxr-x  8 ivang ivang 4096 Dec  5 10:52 setuptools
drwxrwxr-x  2 ivang ivang 4096 Dec  5 10:53 setuptools-65.6.3.dist-info
drwxrwxr-x  3 ivang ivang 4096 Dec  5 10:53 zope
drwxrwxr-x  2 ivang ivang 4096 Dec  5 10:53 zope.interface-5.5.2.dist-info
```

>Within this point you may install all the dependencies at once and especifying versions, if required, according to your needs.
>e.g. `pip install --target ./package <package_name_1>==v.v <package_name_2>==v.v`

#### 6) Create a deployment package with the installed libraries at the root.

We execute the following command from within the "package" directory (note the "." at the end of the command) created and also generate the package zip file "my_function_package.zip" inside the working directory created in step 2.

First,
```
(eclipse) astra_streaming_function $ cd package 
```
Then,
```
(eclipse) astra_streaming_function/package $ zip -r /home/ivang/astra_streaming_function/my_function_package.zip . 
```
```
adding: six-1.16.0.dist-info/ (stored 0%)
adding: six-1.16.0.dist-info/LICENSE (deflated 41%)
adding: six-1.16.0.dist-info/METADATA (deflated 55%)
adding: six-1.16.0.dist-info/INSTALLER (stored 0%)
....
adding: dateutil/tz/__pycache__/win.cpython-38.pyc (deflated 52%)
adding: dateutil/tz/__pycache__/_factories.cpython-38.pyc (deflated 54%)
adding: __pycache__/ (stored 0%)
adding: __pycache__/six.cpython-38.pyc (deflated 58%)
adding: six.py (deflated 76%)
```

#### 7) Add my_astra_function.py file to the zip file.

First we move back to the working directory
```
(eclipse) astra_streaming_function/package $ cd ..
```

Once moved back, we execute:
```
(eclipse) astra_streaming_function $ zip my_function_package.zip my_astra_function.py
```
```
 adding: my_astra_function.py (deflated 45%)

```
The final result and the structure of the working directory as follows:
```
(eclipse) astra_streaming_function $ ls -la
```

```
-rw-rw-r--  1 ivang ivang      394 Dec  5 10:47 my_astra_function.py
-rw-rw-r--  1 ivang ivang 23509789 Dec  5 10:58 my_function_package.zip
drwxrwxr-x 16 ivang ivang     4096 Dec  5 10:53 package
```
