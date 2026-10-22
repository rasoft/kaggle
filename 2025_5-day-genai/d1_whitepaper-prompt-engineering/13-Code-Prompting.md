# Code prompting

代码提示

Gemini focuses primarily on text-based prompts, which also includes writing prompts for returning code. Let’s go to the Vertex AI Studio and test these prompts to look at some coding examples.

Gemini 主要面向基于文本的提示 (Prompt)，其中也包括为了返回代码而写的提示。我们到 Vertex AI Studio 里试这些提示，看一些编码例子。

---

## Prompts for writing code

用于写代码的提示

Gemini can also be a developer and help you with writing code in any programming language of choice. As a developer this can help you speed up the process of writing code.

Gemini 也可以当一名开发者，帮你用任意选定的编程语言写代码。作为开发者，这能帮你加快写代码的过程。

Imagine a folder on your machine with hundreds of files that needs to be renamed. Renaming each file would take you a lot of time. You know a little Bash, and could write a script to automate this, but that may also take awhile. So let’s write a prompt. You can write the prompt in the public consumer chatbot Gemini, or if you are more concerned about confidentiality, you can write these prompts within your Google Cloud account and open Vertex AI Studio. The advantage of Vertex AI Studio is that you can configure the temperature etc.

想象你机器上有一个文件夹，里面几百个文件需要重命名。逐个重命名会花很多时间。你懂一点 Bash，可以写个脚本来自动化，但那也可能要一会儿。所以我们写一条提示。你可以在面向公众的消费级聊天机器人 Gemini 里写这条提示；如果更在意保密，可以在你的 Google Cloud 账号里写这些提示，并打开 Vertex AI Studio。Vertex AI Studio 的好处是你可以配置温度 (temperature) 等项。

| | |
| --- | --- |
| **Name** | 1_bash_rename_files_in_folder |
| **Goal** | Write a prompt to write code in Bash to rename files in a folder. |
| **Model** | gemini-pro |
| **Temperature** | 0.1 |
| **Token Limit** | 1024 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**Prompt**

```text
Write a code snippet in Bash, which asks for a folder name.
Then it takes the contents of the folder and renames all the
files inside by prepending the name draft to the file name.
```

**Output**

```bash
#!/bin/bash
# Ask for the folder name
echo "Enter the folder name: "
read folder_name
# Check if the folder exists
if [ ! -d "$folder_name" ]; then
  echo "Folder does not exist."
  exit 1
fi
# Get the list of files in the folder
files=( "$folder_name"/* )
# Rename each file by prepending "draft" to the file name
for file in "${files[@]}"; do
  new_file_name="draft_$(basename "$file")"
  mv "$file" "$new_file_name"
done
echo "Files renamed successfully."
```

**Table 16. Using Gemini to program code**

表 16：用 Gemini 编写代码。

| | |
| --- | --- |
| **名称** | 1_bash_rename_files_in_folder |
| **目标** | 写一条提示，用 Bash 写代码，重命名文件夹里的文件。 |
| **模型** | gemini-pro |
| **温度** | 0.1 |
| **词元 (token) 上限** | 1024 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**提示**

写一段 Bash 代码。它先询问文件夹名称，然后取出该文件夹的内容，给里面所有文件的文件名前面加上 draft。

That seems like good code to me - it’s even documented! However, since LLMs can’t reason, and repeat training data, it’s essential to read and test your code first.

这段代码在我看来不错——甚至还有注释！不过，既然大语言模型 (LLM) 不能推理 (Reasoning)，而且会重复训练数据，就一定要先阅读并测试你的代码。

The moment we are all waiting for, does it really work?

大家等的那一刻到了：它真的能用吗？

Let’s try it first with a test folder with only a few files in it, which will need to be renamed from filename.txt to draft_filename.txt.

先用一个只有几个文件的测试文件夹试一试。文件要从 filename.txt 重命名为 draft_filename.txt。

1. Copy the output from Table 16 (without the ```bash ``` text wrapper), and paste it in a new file called: “rename_files.sh”.

把表 16 的输出复制出来（不要 ```bash ``` 这层文本包装），粘贴到一个名为 “rename_files.sh” 的新文件里。

2. Open a terminal window and type: . rename_files.sh. It will ask to enter a folder name, e.g. test. and hit enter.

打开一个终端窗口，输入：`. rename_files.sh`。它会要求输入文件夹名称，例如 test，然后按回车。

3. The script seems to run fine. You will see the message: Files renamed successfully. When you look into the test folder, notice that all the files were perfectly renamed to draft_filename.txt.

脚本看起来运行正常。你会看到消息：Files renamed successfully。再看测试文件夹，会发现所有文件都被完好地重命名为 draft_filename.txt。

It worked!

它成功了！

---

## Prompts for explaining code

用于解释代码的提示

As a developer when you work in teams you have to read someone else’s code. Gemini can help you with this as well. Let’s take the code output from Table 16, remove the comments and ask the large language model to explain what’s happening, See Table 17:

作为开发者，在团队里工作时你得读别人的代码。Gemini 也可以帮你做这件事。我们取表 16 输出的代码，去掉注释，再请大语言模型解释发生了什么。见表 17：

| | |
| --- | --- |
| **Name** | 1_bash_explain_the_code |
| **Goal** | Write a prompt to explain Bash code |
| **Model** | gemini-pro |
| **Temperature** | 0.1 |
| **Token Limit** | 1024 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**Prompt**

````text
Explain to me the below Bash code:
```
#!/bin/bash
echo "Enter the folder name: "
read folder_name
if [ ! -d "$folder_name" ]; then
echo "Folder does not exist."
exit 1
fi
files=( "$folder_name"/* )
for file in "${files[@]}"; do
new_file_name="draft_$(basename "$file")"
mv "$file" "$new_file_name"
done
echo "Files renamed successfully."
```
````

**Output**

```text
This Bash script performs the following tasks:
1. User Input:
- It prompts the user to enter a folder name using the `echo` and `read`
commands. The entered folder name is stored in the `folder_name` variable.
2. Folder Existence Check:
- It checks if the folder with the specified name exists using the `[ ! -d
"$folder_name" ]` condition. If the folder does not exist, it displays an error
message (“Folder does not exist.”) and exits the script with an exit code of 1.
3. File Listing:
- It lists all the files inside the specified folder using the `files=( "$folder_name"/* )`
command. This creates an array called `files` containing the paths
to all the files in the folder.
4. File Renaming:
- It iterates through each file in the `files` array using a `for` loop.
- For each file, it generates a new file name using the `new_file_name="draft_$(basename "$file")"`
command. This new file name is created by prefixing the original file name with the string “draft_”.
- It then renames the file using the `mv "$file" "$new_file_name"` command,
which moves the file to the new file name.
5. Success Message:
- After renaming all the files, it displays a success message (“Files renamed
successfully.”) to indicate that the renaming operation was successful.
```

**Table 17. A prompt for explaining code**

表 17：一条用来解释代码的提示。

| | |
| --- | --- |
| **名称** | 1_bash_explain_the_code |
| **目标** | 写一条提示来解释 Bash 代码 |
| **模型** | gemini-pro |
| **温度** | 0.1 |
| **词元上限** | 1024 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**提示**

给我解释下面这段 Bash 代码。代码与表 16 的脚本相同，只是去掉了注释：询问文件夹名，检查文件夹是否存在，列出文件，给每个文件名前加上 draft_，再移动文件，最后打印成功消息。

**输出**

这个 Bash 脚本做下面这些事：
1. 用户输入：
- 它用 `echo` 和 `read` 命令提示用户输入文件夹名称。输入的名称存在变量 `folder_name` 里。
2. 检查文件夹是否存在：
- 它用条件 `[ ! -d "$folder_name" ]` 检查指定名称的文件夹是否存在。如果不存在，就显示错误信息（“Folder does not exist.”），并以退出码 1 退出脚本。
3. 列出文件：
- 它用 `files=( "$folder_name"/* )` 列出指定文件夹里的所有文件。这会创建一个名为 `files` 的数组，里面是文件夹中所有文件的路径。
4. 重命名文件：
- 它用 `for` 循环遍历 `files` 数组里的每个文件。
- 对每个文件，用 `new_file_name="draft_$(basename "$file")"` 生成新文件名。新文件名是在原文件名前加上字符串 “draft_”。
- 然后用 `mv "$file" "$new_file_name"` 重命名，把文件移到新文件名。
5. 成功消息：
- 全部重命名之后，显示成功消息（“Files renamed successfully.”），表示重命名操作成功。

---

## Prompts for translating code

用于翻译代码的提示

The bash code from Table 16 seems to work fine. However this script could really be reusable when it would prompt me for file names, ideally it should work as a separate application with an UI. As a starting point, Python would be a better language for a (web) application than Bash. LLMs can help with translating code from one language to another. See the example in Table 18:

表 16 的 Bash 代码看起来能正常工作。不过，如果脚本会向我询问文件名，它会真正可复用；理想情况下它应作为带界面的独立应用来工作。作为起点，做（Web）应用时 Python 比 Bash 更合适。大语言模型可以帮助把代码从一种语言翻译成另一种。见表 18 的例子：

| | |
| --- | --- |
| **Name** | 1_python_rename_files |
| **Goal** | Write a prompt to translate Bash code to Python |
| **Model** | gemini-pro |
| **Temperature** | 0.1 |
| **Token Limit** | 1024 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**Prompt**

```text
Translate the below Bash code to a Python snippet.
```

followed by the Bash script from Table 17.

提示正文是「把下面的 Bash 代码翻译成一段 Python」，后面接表 17 里的那段 Bash 脚本。

**Output**

```python
import os
import shutil
# Get the folder name from the user
folder_name = input("Enter the folder name: ")
# Check if the folder exists
if not os.path.isdir(folder_name):
    print("Folder does not exist.")
    exit(1)
# Get a list of all files in the folder
files = os.listdir(folder_name)
# Iterate over the files
for file in files:
    # Create a new file name with the prefix "draft_"
    new_file_name = f"draft_{file}"
# Move the file to the new name
shutil.move(os.path.join(folder_name, file),
            os.path.join(folder_name, new_file_name))
# Print a success message
print("Files renamed successfully.")
```

**Table 18. A prompt for translating code from Bash to Python**

表 18：一条把代码从 Bash 翻译成 Python 的提示。印刷输出里，`shutil.move` 的缩进落在 `for` 循环之外。

Read and review the code. Copy the output from the prompt and paste it into a new file: file_renamer.py. Test the code by opening a Terminal window, and execute the following command python file_renamer.py.

阅读并审阅代码。把提示的输出复制出来，粘贴到新文件 file_renamer.py。打开终端窗口，执行命令 `python file_renamer.py` 来测试代码。

NOTE: When prompting for (Python) code in the Language Studio in Vertex AI, you will have to click on the ‘Markdown’ button. Otherwise you will receive plain text which is missing the proper indenting of lines, which is important for running Python code.

注意：在 Vertex AI 的 Language Studio 里提示生成（Python）代码时，要点「Markdown」按钮。否则你会得到纯文本，行缩进不正确，而缩进对运行 Python 代码很重要。

---

## Prompts for debugging and reviewing code

用于调试和审阅代码的提示

Let’s manually write some edits to the code of Table 18. It should prompt the user for the filename prefix, and write this prefix in upper case characters. See the example code in Snippet 3, but what a bummer. It now returns Python errors!

我们手工改一改表 18 的代码。它应当提示用户输入文件名前缀，并把这个前缀写成大写。见片段 3 的示例代码，但真倒霉：它现在报出 Python 错误！

```python
import os
import shutil

folder_name = input("Enter the folder name: ")
prefix = input("Enter the string to prepend to the filename: ")
text = toUpperCase(prefix)
if not os.path.isdir(folder_name):
    print("Folder does not exist.")
    exit(1)
files = os.listdir(folder_name)
for file in files:
    new_filename = f"{text}_{file}"
shutil.move(os.path.join(folder_name, file),
            os.path.joi(folder_name, new_file_name))
print("Files renamed successfully.")
```

**Snippet 3. A broken Python script**

片段 3：一段坏掉的 Python 脚本。`toUpperCase` 不是 Python 里的函数，`os.path.joi` 也不是 `os.path.join`，循环里的变量名是 `new_filename`，移动文件时却用了 `new_file_name`。

Doh! That looks like a bug:

唉！这看起来像个缺陷：

```text
The below Python code gives an error:
Traceback (most recent call last):
  File "/Users/leeboonstra/Documents/test_folder/rename_files.py", line 7, in <module>
    text = toUpperCase(prefix)
NameError: name 'toUpperCase' is not defined
```

**Snippet 4. I broke the Python code**

片段 4：我把 Python 代码弄坏了。回溯指向 rename_files.py 第 7 行的 `text = toUpperCase(prefix)`，错误是 `NameError: name 'toUpperCase' is not defined`。

Let’s see if we can ask the large language model to debug and review code. Have a look into Table 19:

看看能不能请大语言模型来调试和审阅代码。见表 19：

| | |
| --- | --- |
| **Name** | 1_python_debug_code |
| **Goal** | Write a prompt to debug and review Python code. |
| **Model** | gemini-pro |
| **Temperature** | 0.1 |
| **Token Limit** | 1024 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**Prompt**

```text
The below Python code gives an error:
Traceback (most recent call last):
  File "/Users/leeboonstra/Documents/test_folder/rename_files.py", line 7, in <module>
    text = toUpperCase(prefix)
NameError: name 'toUpperCase' is not defined
Debug what's wrong and explain how I can improve the code.
```

The prompt then includes the Python from Snippet 3, with comments restored in the paper’s listing.

提示先给出上面的回溯，再要求调试哪里错了，并解释如何改进代码。提示里接着放入片段 3 的 Python，印刷列表中注释被加了回去。

**Output**

```text
The code calls the `toUpperCase` function to convert `prefix` to uppercase, but
that function is not defined. To fix this issue, you can use the `upper()` method of
the string class which converts a given string into uppercase. The modified code
is shown below:
```

```python
import os
import shutil
folder_name = input("Enter the folder name: ")
prefix = input("Enter the string to prepend to the filename: ")
text = prefix.upper()
if not os.path.isdir(folder_name):
    print("Folder does not exist.")
    exit(1)
files = os.listdir(folder_name)
for file in files:
    new_filename = f"{text}_{file}"
shutil.move(os.path.join(folder_name, file),
            os.path.join(folder_name, new_filename))
print("Files renamed successfully.")
```

```text
Additionally, there are a few other improvements that can be made to the code:
1. The file extension of the new filenames is not kept. It’s better to extract the
extension from the original filename and append it to the new filename.
2. The code assumes that there are no spaces in the folder name. However,
it is a good practice to handle spaces gracefully by replacing them with
underscores or hyphens.
3. Using the `f` string syntax for string interpolation is more readable and
concise than the traditional `+` operator.
4. The code doesn’t handle errors that might occur during the renaming process.
It would be better to wrap the `shutil.move` call in a `try...except` block to
catch any potential errors.
Here is the improved code with these suggestions:
```

```python
import os
import shutil
folder_name = input("Enter the folder name: ")
prefix = input("Enter the string to prepend to the filename: ")
if not os.path.isdir(folder_name):
    print("Folder does not exist.")
    exit(1)
files = os.listdir(folder_name)
for file in files:
    ext = os.path.splitext(file)[1]
    new_filename = f"{prefix}_{os.path.splitext(file)[0]}{ext}"
    old_path = os.path.join(folder_name, file)
    new_path = os.path.join(folder_name, new_filename)
    try:
        shutil.move(old_path, new_path)
    except Exception as e:
        print(f"An error occurred while moving the file {file}: {e}")
print("Files renamed successfully.")
```

```text
These improvements make the code more robust and flexible while also making
it easier to read and understand... (The response was truncated because
it has reached the token limit. Try to increase the token limit if you need a
longer response.)
```

**Table 19. A prompt for debugging and reviewing Python code**

表 19：一条用来调试和审阅 Python 代码的提示。模型指出 `toUpperCase` 未定义，建议改用字符串的 `upper()`。它还建议保留扩展名、处理文件夹名里的空格、使用 f 字符串，并把 `shutil.move` 放进 `try...except`。回答因达到词元上限而被截断。

**输出说明**

代码调用 `toUpperCase` 把 `prefix` 转成大写，但该函数没有定义。可以改用字符串的 `upper()` 方法。此外模型还列出四项改进：新文件名没有保留扩展名；代码假设文件夹名里没有空格；f 字符串比 `+` 更可读；重命名过程没有处理错误。改进后的代码更稳健、更灵活，也更容易读。回答在达到词元上限后被截断。

That’s great. Not only did it tell me how to solve the problem, it also figured out that my code had more bugs and how to solve them, too. The last part of the prompt gave suggestions to improve the code in general.

很好。它不但告诉我怎么解决这个问题，还发现我的代码还有更多缺陷，以及怎么修。提示的最后一部分给出了总体上改进代码的建议。

---

## What about multimodal prompting?

多模态提示 (multimodal prompting) 呢？

Prompting for code still uses the same regular large language model. Multimodal prompting is a separate concern, it refers to a technique where you use multiple input formats to guide a large language model, instead of just relying on text. This can include combinations of text, images, audio, code, or even other formats, depending on the model’s capabilities and the task at hand.

为代码写提示，用的仍是同一个常规大语言模型。多模态提示是另一件事：它指用多种输入格式来引导大语言模型，而不只靠文本。视模型能力和手头任务，这可以包括文本、图像、音频、代码，甚至其他格式的组合。
