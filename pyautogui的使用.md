# pyautogui的使用

#### 1.鼠标操作

```
# 获取屏幕宽和高
w,h = pyautogui.size()      

# 在坐标 (1136,706) 位置处使用鼠标左键；默认从鼠标当前坐标位置；button 默认为 "left"，有三个可选值，分别为 "left","middle","right"
pyautogui.click(1136,706,button="left")   
pyautogui.leftClick(x,y)

# 在 (300,400) 坐标处左键双击
pyautogui.click(300, 400,clicks=2, button='left',interval=0.25)  
# 在 (x，y) 坐标处双击操作；button 默认为 "left"，有三个可选值，分别为 "left","middle","right"
pyautogui.doubleClick(x,y,button="left",duration=0.25)

# 在坐标 (1136,706) 位置处使用鼠标右键
pyautogui.click(1136,706,button="right")    
pyautogui.rightClick(x,y)

# 在坐标 (x，y) 位置处使用鼠标中键
pyautogui.middleClick(x,y)

# 按下某个键
pyautogui.mouseDown()       

# 鼠标拖动到坐标 (1566,706) 位置处
pyautogui.moveTo(1566,706,duration=0.2)     

# 松开某个键
pyautogui.mouseUp()
```



#### 2.滚动条操作

```
# 滚动条操作，它只接受一个整数，值为正则往上滚，值为负则往下滚
pyautogui.scroll(-200) 
pyautogui.scroll(200)
'''注意鼠标先点击滚动条'''

```

#### 3.输入操作

```
# 选择输入框
pyautogui.click(624,391) 

# 往输入框输入内容
pyautogui.typewrite("17779828887") 
```

#### 4.键盘操作

```
# 删除一个字符
pyautogui.typewrite(["backspace"])  

# 执行 enter 回车操作
pyautogui.typewrite(["enter"])  

# 先在当前位置光标向左一个字符，接着删除一个字符，再输入 a，再执行 enter 操作;延时 2 秒
pyautogui.typewrite(["left","backspace","a","enter"],"2")
```

| "enter"(或 "return" 或 "\n")           | 回车                                  |
| -------------------------------------- | ------------------------------------- |
| "esc"                                  | ESC键                                 |
| "shiftleft", "shiftright"              | 左右SHIFT键                           |
| "altleft", "altright"                  | 左右ALT键                             |
| "ctrlleft", "ctrlright"                | 左右CTRL键                            |
| "tab" ("\t")                           | TAB键                                 |
| "backspace", "delete"                  | BACKSPACE 、DELETE键                  |
| "pageup", "pagedown"                   | PAGE UP 和 PAGE DOWN键                |
| "home", "end"                          | HOME 和 END键                         |
| "up", "down", "left", "right"          | 箭头键                                |
| "f1", "f2", "f3"….                     | F1…….F12键                            |
| "volumemute", "volumedown", "volumeup" | 有些键盘没有                          |
| "pause"                                | PAUSE键                               |
| "capslock", "numlock", "scrolllock"    | CAPS LOCK, NUM LOCK, 和 SCROLLLOCK 键 |
| "insert"                               | INS或INSERT键                         |
| "printscreen"                          | PRTSC 或 PRINT SCREEN键               |
| "winleft", "winright"                  | Win键                                 |
| "command"                              | Mac OS X command键                    |

#### 5.组合键操作

```
#使用组合键
# alt + a 键进行组合使用
pyautogui.keyDown('alt')
pyautogui.press('a')
pyautogui.keyUp('alt')
# 使用热键
# 调起 qq
pyautogui.hotkey("ctrl","alt","z") 

#调起微信
pyautogui.hotkey("alt","d") 
```



## 处理验证滑块案例

```
import pyautogui
from selenium import webdriver
import time
dr = webdriver.Chrome()
dr.get("https://shopcs.yunyoute.com/login")
dr.maximize_window()
dr.implicitly_wait(10)
time.sleep(2)
pyautogui.click(1136,706,button="left")     # 在坐标(1136,706)位置处进行鼠标左键
pyautogui.mouseDown()       # 按下鼠标键
pyautogui.moveTo(1566,706,duration=0.2)     # 鼠标拖动到坐标(1566,706)位置处
pyautogui.mouseUp()     # 松开鼠标
```

#### 将滑块封装为公共方法

```
"""
文件 Left_slide.py
"""
import pyautogui

def left():
    w,h = pyautogui.size()    # 获取屏幕宽 w 和高 h
    x1 = w * 0.59
    x2 = w * 0.81
    y1 = h * 0.65
    pyautogui.click(x1,y1,button="left")     # 在坐标(1136,706)位置处进行鼠标左键
    pyautogui.mouseDown()       # 按下鼠标键
    pyautogui.moveTo(x2,y1,duration=0.2)     # 鼠标拖动到坐标(1566,706)位置处
    pyautogui.mouseUp()     # 松开鼠标

"""
文件 case.py
"""
from selenium import webdriver
from public.Left_slide import left
import time
dr = webdriver.Chrome()
dr.get("https://shopcs.yunyoute.com/login")
dr.maximize_window()
dr.implicitly_wait(10)
time.sleep(2)
left()        # 调用左滑方法
```

