import os
import shutil
import time

def sl():
    time.sleep(1)

def make_dir(newdir_place_path,name):
    newdirpath = os.path.join(newdir_place_path,name)
    if not os.path.exists(newdirpath):
        os.makedirs(newdirpath)



file1 = input('コピーファイルを作るフォルダのpathを入力(""ありで):')[1:-1]
new_file_plac = input('コピーファイルを作る場所のpathを入力(""ありで)')[1:-1]
new_file_name = input('新しいファイルの名前を入力')
new_file_place = os.path.join(new_file_plac,new_file_name)
n = 1
extention_list = []
while n == 1:
    extention = input('コピーするファイルの拡張子を入力(複数ある場合は、続けて書く。これ以上ない場合は、空白でEnter)')
    if extention == '':
        break
    extention_list.append(extention)
    

ssfile = file1

for exen in extention_list:
    if os.path.exists(ssfile):

        for root,dirs,files in os.walk(ssfile):
            sl()

            for dir in dirs:
                nowpath = os.path.join(root,dir)
                dir_path = os.path.relpath(nowpath,file1)
                make_dir(new_file_place,dir_path)

            for file in files:
                full_path = os.path.join(root,file)
                full_path_file = os.path.relpath(full_path,file1)
                path_place = os.path.join(new_file_place,os.path.relpath(root,file1))

                name,ex = os.path.splitext(file)
                if ex == exen:
                    shutil.copy(full_path,path_place)


    else:
        print('ファイルがありません')
