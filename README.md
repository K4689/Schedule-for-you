# Schedule-for-you
'''
It's a program that I hope will help me making my schedules por University;  it read a txt  where its all the information and the program take that, make all the posibles Schedule for you and select wich one is more near to your necesities'''

#PARTE LOGICA
global cursos
cursos=[]


class Curso:
    def __init__(self,codigo,nombre,creditos):
        self.nombre=nombre
        self.codigo=codigo
        self.creditos=creditos 
        self.clases=[]

    def Nclase (self, NewClase):
        self.clases.append(NewClase)
    
    def __str__(self):
        return 'Nombre:'+self.nombre+'\nCodigo:'+self.codigo+'\nCreditos:'+self.creditos
        
class Clase(Curso):
    def __init__(self,profesor,codigoC,Dhoradia):
        self.profesor=profesor
        self.codigoC=codigoC
        self.Dhoradia=Dhoradia #esto es un diccionario 

    def __str__ (self):
        return '- Profesor:'+self.profesor+'\n- Codigo:'+self.codigoC+'\n- Horario:'+str(self.Dhoradia)


#FUNCIONES MENUw

def IngresarInfoM():
    print("*ok vamos a agregar la info")
    op='1'
    print("¿Desee ingrear un curso o una clase?(1/2)")
    respuesta=input()
    if respuesta=='1' :
        print("ok, vas a ingresar una curso")
        nombre=input("Ingrese el nombre de la clase:")
        codigo=input("Ingrese el codigo de la clase:")
        creditos= input("Ingrese los creditos de la clase:")
        Ncurso=Curso(codigo,nombre,creditos)
        cursos.append(Ncurso)
        print("Por favor ingrese las clases del curso")
        codigo=input("Ingrese el codigo:")
        profesor=input("Ingrese el profesor:")
        dias=int(input("Ingrese cuantos dias va a tener la clase:"))
        horario={}
        for i in range(dias):
            dia=input("Ingrese el dia:")
            hora=input("Ingrese las horas:")
            horario.setdefault(dia,hora)
        Nclase=Clase(profesor,codigo,horario)
        Ncurso.Nclase(Nclase)
    return op 

def IngresarInfoA():
    archivo= open("Info.txt",'rt')
    contenido=archivo.readlines()
    for lineas in contenido:
        for letra in range(len(lineas)):
            try:
                curso=''
                codigo=''
                creditos=''
                horario={}
                if lineas[letra]=='*':  #nuevaclase
                    letra+=1
                    while lineas[letra]!='.':
                        curso+=lineas[letra]
                        letra+=1
                    letra+=1
                    while lineas[letra]!='.':
                        codigo+=lineas[letra]
                        letra+=1
                    letra+=1
                    creditos=lineas[letra]
                    Ncurso=Curso(codigo,curso,creditos)
                    cursos.append(Ncurso)
                elif lineas[letra]=='-': #nuevo curso
                    codigo=''
                    profesor=''
                    letra+=1
                    while lineas[letra]!='.':
                        codigo+=lineas[letra]
                        letra+=1
                    letra+=1
                    while lineas[letra]!='.':
                        profesor+=lineas[letra]
                        letra+=1
                    while lineas[letra]!='_': #horario
                        dia=''
                        horaT=''
                        hora=[]
                        letra+=1
                        while lineas[letra]!='(':
                            dia+=lineas[letra]
                            letra+=1
                        letra+=1
                        while lineas[letra]!='-':
                            horaT+=lineas[letra]
                            letra+=1 
                        letra+=1
                        hora.append(int(horaT))
                        horaT=''
                        while lineas[letra]!=')':
                            horaT+=lineas[letra]
                            letra+=1  
                        hora.append(int(horaT))  
                        horario.setdefault(dia,hora)
                        letra+=1
                    Nclase=Clase(profesor,codigo,horario)
                    Ncurso.Nclase(Nclase)
            except:
                pass
                
    print("Clases Registradas")

def VerInfo():
    op='2'
    curso=0
    while curso<len(cursos):
        print("\n","***Informacion Cursos***","\n")
        print(cursos[curso])
        respuesta=input("Desea ver las clases del curso?(s/n)")
        if respuesta=='s':
            print("-\n","**Informacion clases***")
            for cla in range(len(cursos[curso].clases)):  
                print("\nClase",cla+1)
                print(cursos[curso].clases[cla])
        curso+=1
    return op

def ModificarInfo():
    print("*Para modificar la informacion")
    op='3'
    return op



def BuscarInfo(): #esta funcion le das el codigo de la clase y te retorna informacion 
    # mas precisa de la clases y el curso
    print("hey")


def TerminarP ():
    print("*Salir del programa")
    op='5'
    return op


def menu (opcion):
    
    if opcion==1: op= IngresarInfoM()
    elif opcion==2: op= VerInfo()
    elif opcion==3:  op= ModificarInfo()
    elif opcion==4:   op=CrearHorarios()
    elif opcion==5:    op= TerminarP() 
    
    return op 


#SECCION DE PRUEBA DE FUNCIONES 
print("INICIA")
IngresarInfoA()




'''
print("Iniciar programa....(s/n)")
correr=input()
if correr=='s':
    funcionando=True
else:
    funcionando=False 

while (funcionando):
    
    print("***CREADOR DE HORARIOS***")
    print("Menu","1.Ingresar Info","2.Ver info","3.Modificar info","4.Crear Horarios","5.Salir",sep="\n")
    opcion=int(input())
    opcion1 = menu(opcion)
   
    if opcion1=="5":
        funcionando=False 
    

print("Gracias por haber usado ScheduleMaker <3")
'''



