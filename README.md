# doors

#ИНТЕРФЕЙС

import cv2
import numpy as np
from matplotlib import pyplot as plt
from PIL import Image, ImageChops  # ImageDraw
import math, operator
from functools import reduce
from PyQt5 import QtCore, QtGui, QtWidgets
import pygame
import pandas as pd
import time
g=pd.read_excel('3.xlsx')
t=pd.read_excel('2.xlsx')
dor=pd.read_excel('4.xlsx')

class Ui_MainWindow(object):
    def setupUi(self, MainWindow):
        MainWindow.setObjectName("MainWindow")
        MainWindow.resize(802, 578)
        MainWindow.setStyleSheet("background-color:darkgray")
        self.centralwidget = QtWidgets.QWidget(MainWindow)
        self.centralwidget.setObjectName("centralwidget")
        self.pushButton = QtWidgets.QPushButton(self.centralwidget)
        self.pushButton.setGeometry(QtCore.QRect(20, 30, 321, 71))
        font = QtGui.QFont()
        font.setFamily("Onyx")
        font.setPointSize(14)
        self.pushButton.setFont(font)
        self.pushButton.setStyleSheet("background-color:firebrick")
        self.pushButton.setObjectName("pushButton")
        self.pushButton_2 = QtWidgets.QPushButton(self.centralwidget)
        self.pushButton_2.setGeometry(QtCore.QRect(20, 140, 321, 71))
        font = QtGui.QFont()
        font.setFamily("Onyx")
        font.setPointSize(14)
        self.pushButton_2.setFont(font)
        self.pushButton_2.setStyleSheet("background-color:firebrick")
        self.pushButton_2.setObjectName("pushButton_2")
        self.pushButton_3 = QtWidgets.QPushButton(self.centralwidget)
        self.pushButton_3.setGeometry(QtCore.QRect(20, 260, 321, 71))
        font = QtGui.QFont()
        font.setFamily("Onyx")
        font.setPointSize(14)
        self.pushButton_3.setFont(font)
        self.pushButton_3.setStyleSheet("background-color:firebrick")
        self.pushButton_3.setObjectName("pushButton_3")
        self.label_2 = QtWidgets.QLabel(self.centralwidget)
        self.label_2.setGeometry(QtCore.QRect(430, 10, 401, 241))
        self.label_2.setText("")
        self.label_2.setPixmap(QtGui.QPixmap("rjd.png"))
        self.label_2.setObjectName("label_2")
        self.listWidget = QtWidgets.QListWidget(self.centralwidget)
        self.listWidget.setGeometry(QtCore.QRect(0, 360, 811, 221))
        self.listWidget.setStyleSheet("border-style: solid; border-width: 1px; border-color: black; background-color:lightgray;")
        self.listWidget.setObjectName("listWidget")
        self.pushButton_4 = QtWidgets.QPushButton(self.centralwidget)
        self.pushButton_4.setGeometry(QtCore.QRect(380, 260, 171, 71))
        font = QtGui.QFont()
        font.setFamily("Onyx")
        font.setPointSize(14)
        self.pushButton_4.setFont(font)
        self.pushButton_4.setStyleSheet("background-color:firebrick")
        self.pushButton_4.setObjectName("pushButton_4")
        MainWindow.setCentralWidget(self.centralwidget)
        self.pushButton.clicked.connect(self.db)
        self.pushButton_2.clicked.connect(self.sound)
        self.pushButton_4.clicked.connect(self.clearr)
        self.pushButton_3.clicked.connect(self.cum)
        self.pushButton_3.clicked.connect(self.cam)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)
    def sound(self):
        self.listWidget.clear()
        pygame.mixer.init()
        pygame.mixer.music.load("ost.mp3")
        pygame.mixer.music.play()
        time.sleep(5)
        d = t['Разрешение'] = t.apply(lambda row: row.Ст == 1, axis=1)
        list = [d]
        a = "".join(map(str, list))
        self.listWidget.addItem(a)

    def cam(self):
        self.listWidget.clear()
        time.sleep(10)

        ichod_1 = Image.open('gs1.jpg')
        ichod_2 = Image.open('gs27.jpg')
        poick_photo = Image.open('gs1.jpg')
        h = ImageChops.difference(ichod_1, poick_photo).histogram()
        h2 = ImageChops.difference(ichod_2, poick_photo).histogram()
        df = math.sqrt(reduce(operator.add, map(lambda h, i: h * (i ** 2), h, range(256))) / (float(ichod_1.size[0])
                                                                                              * ichod_1.size[1]))
        df2 = math.sqrt(
            reduce(operator.add, map(lambda h2, i: h2 * (i ** 2), h2, range(256))) / (float(ichod_2.size[0])
                                                                                      * ichod_2.size[1]))
        print(df)
        print(df2)
        if df2 <= df:
            k = df2
        else:
            k = df
        print(k)
        if (k > 6.0):
            poick_photo.show()
            text = "\n\n\n\t\t\t\tУгроза обнаружена!!!"
            t = [text]
            a = "".join(map(str, t))
            self.listWidget.addItem(a)
        else:
            poick_photo.show()
            text = "\n\n\n\t\t\t\tУгроз не обнаружено!!!"
            t = [text]
            a = "".join(map(str, t))
            self.listWidget.addItem(a)
        return df

    def cum(self):
        self.listWidget.clear()
        self.cravn()
        ichod_1 = Image.open('gs1.jpg')
        ichod_2 = Image.open('gs27.jpg')
        poick_photo = Image.open('gs13.jpg')
        h = ImageChops.difference(ichod_1, poick_photo).histogram()
        h2 = ImageChops.difference(ichod_2, poick_photo).histogram()
        df = math.sqrt(reduce(operator.add, map(lambda h, i: h * (i ** 2), h, range(256))) / (float(ichod_1.size[0])
                                                                                              * ichod_1.size[1]))
        df2 = math.sqrt(
            reduce(operator.add, map(lambda h2, i: h2 * (i ** 2), h2, range(256))) / (float(ichod_2.size[0])
                                                                                      * ichod_2.size[1]))
        print(df)
        print(df2)
        if df2 <= df:
            k = df2
        else:
            k = df
        print(k)
        if (k > 6.0):
            poick_photo.show()
            text = "\n\n\n\t\t\t\tУгроза обнаружена!!!"
            t = [text]
            a = "".join(map(str, t))
            self.listWidget.addItem(a)
        else:
            poick_photo.show()
            text = "\n\n\n\t\t\t\tУгроз не обнаружено!!!"
            t = [text]
            a = "".join(map(str, t))
            self.listWidget.addItem(a)
        return df


    def clearr(self):
        self.listWidget.clear()
        time.sleep(5)
        text = "\n\n\n\t\t\t\tМожно трогаться!"
        t = [text]
        a = "".join(map(str, t))
        self.listWidget.addItem(a)
    def db(self):
        self.listWidget.clear()
        pygame.mixer.init()
        pygame.mixer.music.load("door.mp3")
        pygame.mixer.music.play()
        time.sleep(3)
        d = g['Разрешение'] = g.apply(lambda row: row.Ст == 1, axis=1)
        list = [d]
        a="".join(map(str, list))

        self.listWidget.addItem(a)
    def retranslateUi(self, MainWindow):
        _translate = QtCore.QCoreApplication.translate
        MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
        self.pushButton.setText(_translate("MainWindow", "Проверка дверей"))
        self.pushButton_2.setText(_translate("MainWindow", "Устранение ошибки"))
        self.pushButton_3.setText(_translate("MainWindow", "Проверка платформы"))
        self.pushButton_4.setText(_translate("MainWindow", "Завершить"))

    def cravn(self):
        # plt.figure(figsize=(16, 16))
        photos = '13.png'
        img_gs = cv2.imread(photos, cv2.IMREAD_GRAYSCALE)  # IMREAD_GRAYSCALE
        cv2.imwrite('gs13.jpg', img_gs)

    # df_photos = 'gs1.jpg'
    # edges = cv2.Canny(img_gs, 100,200)

    def works(self):  # im1, im2
        ichod_1 = Image.open('gs1.jpg')
        ichod_2 = Image.open('gs27.jpg')
        poick_photo = Image.open('gs13.jpg')
        h = ImageChops.difference(ichod_1, poick_photo).histogram()
        h2 = ImageChops.difference(ichod_2, poick_photo).histogram()
        # poick_photo.show()
        df = math.sqrt(reduce(operator.add, map(lambda h, i: h * (i ** 2), h, range(256))) / (float(ichod_1.size[0])
                                                                                              * ichod_1.size[1]))
        df2 = math.sqrt(
            reduce(operator.add, map(lambda h2, i: h2 * (i ** 2), h2, range(256))) / (float(ichod_2.size[0])
                                                                                      * ichod_2.size[1]))
        print(df)
        print(df2)
        if df2 <= df:
            k = df2
        else:
            k = df
        print(k)
        if (k > 6.0):
            poick_photo.show()
        else:
            print("Угроз не обнаружено")
        return df



if __name__ == "__main__":
    import sys
    app = QtWidgets.QApplication(sys.argv)
    MainWindow = QtWidgets.QMainWindow()
    ui = Ui_MainWindow()
    ui.setupUi(MainWindow)
    MainWindow.show()
    sys.exit(app.exec_())
    
#АЛГОРИТМ ОБНАРУЖЕНИЯ УГРОЗЫ
import cv2
import numpy as np
from matplotlib import pyplot as plt
from PIL import Image, ImageChops #ImageDraw
import math, operator
from functools import reduce

photos = '21.png'
def cravn():
   # plt.figure(figsize=(16, 16))
    img_gs = cv2.imread(photos, cv2.IMREAD_GRAYSCALE) #IMREAD_GRAYSCALE
    cv2.imwrite('gs21.jpg', img_gs)

    name_photo = '21.png'
    pustoi_1 = Image.open('red_1.jpg')
    pustoi_2 = Image.open('red_27.jpg')
    img1 = cv2.imread(name_photo, 1)
    hsv = cv2.cvtColor(img1, cv2.COLOR_BGR2HSV)

    lower_red = np.array([0, 50, 50])
    upper_red = np.array([10, 255, 255])

    lower_red2 = np.array([170, 50, 50])
    upper_red2 = np.array([180, 255, 255])
    mask = cv2.inRange(hsv, lower_red, upper_red)
    res = cv2.bitwise_and(img1, img1, mask=mask)
    mask2 = cv2.inRange(hsv, lower_red2, upper_red2)
    res2 = cv2.bitwise_and(img1, img1, mask=mask2)

    img1 = res + res2
        #img2 = res + res2

    cv2.imwrite('red_21.jpg', img1)
    #fg = cv2.imwrite('red_9.jpg', img1)
    #cv2.imshow('Original', img1)
    #cv2.imshow('res3', img1)
#
    resultat = Image.open('red_1.jpg')
    resultat.show()

    imgen = Image.open('red_21.jpg')
    cv2.waitKey(0)
    cv2.destroyAllWindows()

    h = ImageChops.difference(pustoi_1, imgen).histogram()
    h2 = ImageChops.difference(pustoi_2, imgen).histogram()
    #poick_photo.show()
    df = math.sqrt(reduce(operator.add, map(lambda h, i: h * (i ** 2), h, range(256))) / (float(pustoi_1.size[0])
                                                                                          * pustoi_1.size[1]))
    df2 = math.sqrt(reduce(operator.add, map(lambda h2, i: h2 * (i ** 2), h2, range(256))) / (float(pustoi_2.size[0])
                                                                                              * pustoi_2.size[1]))
    print(df)
    print(df2)

    if df2 <= df:
        k_2 = df2
    else:
        k_2 = df

    ichod_1 = Image.open('gs1.jpg')
    ichod_2 = Image.open('gs27.jpg')
    poick_photo = Image.open('gs21.jpg')
    h_ = ImageChops.difference(ichod_1, poick_photo).histogram()
    h2_ = ImageChops.difference(ichod_2, poick_photo).histogram()
    #poick_photo.show()
    df_ = math.sqrt(reduce(operator.add, map(lambda h_, i: h_*(i**2), h_, range(256))) / (float(ichod_1.size[0])
                                                                                          * ichod_1.size[1]))
    df2_ = math.sqrt(reduce(operator.add, map(lambda h2_, i: h2_*(i**2), h2_, range(256))) / (float(ichod_2.size[0])
                                                                                              * ichod_2.size[1]))
    print(df_)
    print(df2_)
    if df2_ <= df_:
        k = df2_+k_2
    else:
        k = df_+k_2
    print(k)
    if (k > 11.0):
        resultat = Image.open(photos)
        resultat.show()
    else:
        print("Угроз не обнаружено")
    return df_

cravn()

    
