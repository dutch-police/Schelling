import random

n = 10   #Размер будущего поля (n на n)

m=[0]*n**2  #Создаем одномерный лист и заполняем его согласно заданию: -1 - один цвет, 1 - другой цвет, 0 - пустая клетка

for i in range (    round(n*n*0.45)   ):
    m[i] = -1
for i in range (    round(n*n*0.45),2*round(n*n*0.45)   ):
    m[i] = 1

random.shuffle(m)   # Перемешиваем обеъкты, имитируя случайное заполнение


z = [[0 for i in range(n)] for j in range(n)]  # Создаем двумерную матрицу. Это будет основная матрица

for i in range (n):
    for j in range (n):
        z[i][j] = m[i*n + j] # Переносим объекты



#Функция расчета счастливых клеток, которые будут записаны в happines_matr.
#' + ' клетка счастливая, ' - ' клетка несчастливая, ' 0 ' клетка пустая.
def HeighbrsSumMatr (z,n):
    temp = [[0 for i in range(n+2)] for j in range(n+2)]  #Эта матрица нужна, чтобы корректно считались краевые элементы.
    happines_matr = [[' 0 ' for i in range(n)] for j in range(n)]

    for i in range (n):
        for j in range (n):
            temp[i+1][j+1] = z[i][j] #Все элементы сдвигаем на +1 по верт и +1 по горизонтали, по краям нули.

    switch= { -1:{-1:1, 1:0, 0:0} , 1:{-1:0, 1:1, 0:0} , 0:{-1:0, 1:0, 0:0} }
    
    for i in range(n):
        for j in range(n):
            a=0
            
            #Создаим лист соседей для клетки i,j. Помним что в матрице все элементы сдвинулись.
            neighbours_list = [  temp[i][j],temp[i][j+1],temp[i][j+2],temp[i+1][j],
                              temp[i+1][j+2],temp[i+2][j],temp[i+2][j+1],temp[i+2][j+2] ]
            
            #Словарь switch, позволит избежать зеленых условий
            '''if z[i][j] == -1:
                for x in neighbours_list:
                    if x == -1:
                        a +=1

            if z[i][j] == 1:
                for x in neighbours_list:
                    if x == 1:
                        a +=1'''      
            for x in neighbours_list:
                a += switch[ z[i][j] ][ x ]

            
            if a>=2:
                happines_matr[i][j]=' + '
            else:
                happines_matr[i][j]=' - '

            if z[i][j] == 0:
                happines_matr[i][j]=' 0 '
                
    
    return happines_matr

#Функция, меняющая случайную несчастливую клетку, и пустую местами
def Swapper (z,n,happines_matr):
    unhappy_list = []
    zeros_list = []
    for i in range (n):
        for j in range(n):
            if happines_matr[i][j]== ' - ' :
                unhappy_list.append( [i,j,z[i][j]] )
                
            if z[i][j]== 0:
                zeros_list.append ( [i,j,z[i][j]] )
        
    global unhappy_elem,zeros_elem
    unhappy_elem = random.choice(unhappy_list)
    zeros_elem =random.choice(zeros_list)

    z[  unhappy_elem[0] ][  unhappy_elem[1] ] = zeros_elem[2]
    z[  zeros_elem[0] ][  zeros_elem[1] ] = unhappy_elem[2]
    
    return z                 


#Функция красиво печатает матрицу, цифра под цифрой
def MatrPrinter (z,n):
    switch = { -1:'-1 ', 1:' 1 ', 0:' 0 ' }
    
    for i in range (n):
        for j in range(n):
            print (switch[ z[i][j] ],'',end="  ")
        print(sep='')




for times in range (50):
    try:
        print('Шаг ',times)

        MatrPrinter (z,n)    
        happines_matr=HeighbrsSumMatr(z,n)
        print('\n')
        
        for i in range (n):    
            print ('   '.join(happines_matr[i]))
            
        z = Swapper (z,n,happines_matr)
    except IndexError:
        print('Все клетки счастливы')
        break
#    print('Меняем местами ',unhappy_elem,' и ',zeros_elem)
    
    print('###############################################################')

