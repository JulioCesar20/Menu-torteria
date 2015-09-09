# Menu-torteria

#include <stdio.h>
#include<stdlib.h>
#include<locale.h>
#define p printf
#define s scanf


struct menu
{
	int precio, unidades;	
};

int menu (int );
char opcion,res;
FILE *ap;

main()
{
	setlocale(LC_ALL,"esm");
	char res, cin[100];
	int total=0,i,ang,j;
	struct menu a[4];
	
	for(i=0;i<4;i++) //Aqui ponemos las unidades de cada producto en la lista
	    a[i].unidades=0;
	
	a[0].precio=40;
	a[1].precio=15;
	a[2].precio=55;
	a[3].precio=10;
	//Con esto le decimos a la estructura cual sera el precio de cada producto
	
	do
	{                 
	   
	    
	    do
	      { 
	      	ap=fopen("menu.txt","r");	//abre el menu

			    if (ap==NULL)
					{
						printf("No se encuentra el archivo");
					}
			    else
				  {
		          while(feof(ap)==NULL)       
		               {
		               		for(j=0;j<2;j++)
						   	{
		                    	cin[j]=fgetc(ap);  //hace grupos de dos caracteres
		               			printf("%c",cin[j]);
		               	    }
		                    if(cin[0]=='4' && cin[1]=='0')  //verfica sea 40
							  {
		                        ang=atoi(cin);              //transformación de char a int
					            a[0].precio=ang;             //guardar dato 
					          }
					        if(cin[0]=='1' && cin[1]=='5')  //verifica sea 15
					          {
		                        ang=atoi(cin);
					            a[1].precio=ang;
					          }
					   	    if(cin[0]=='5' && cin[1]=='5')  //verifica sea 55
					          {
		                        ang=atoi(cin);
					            a[2].precio=ang;
					          }
					        if(cin[0]=='1' && cin[1]=='0')  //verifica sea 10
					          {
		                        ang=atoi(cin);
					            a[3].precio=ang;
					          }
		               }
		          fclose(ap);
	              }
	             printf(" \n\n¿Cual es su orden?: " );
          	   	 fflush(stdin);
                 opcion=getchar();
	      		system("CLS");
	      }
	    while(opcion!='a'&& opcion!='A' && opcion!='b'&& opcion!='B'&& opcion!='c'&& opcion!='C'&& opcion!='d'&& opcion!='D'&& opcion!='e'&& opcion!='E');   
	    
	    if(opcion=='e' || opcion=='E') 
		    {  
			 	p("\n\n Tu pedido fue el siguiente:\n" 
		   		  "-------------------------\n"   );       
		    	p(" %d Cubana   \n", a[0].unidades);
		    	p(" %d Jamon    \n", a[1].unidades); 
		    	p(" %d Especial \n", a[2].unidades); 
				p(" %d Refresco \n", a[3].unidades);                   
		        p("\n El monto a pagar es de: %d\n\n", total);
				break;
			}//Esta parte muestra al cliente cual fue su orden y el total a pagar, para posteriormente, salirse del programa.
	        
	switch(opcion) 
	      {
		   case 'a': case'A':    
				total+=a[0].precio;
				a[0].unidades++;				
	        break;
	        
	        case 'b': case'B':
				 total+=a[1].precio;
				 a[1].unidades++;
			break;
			
			case 'c': case'C':
				  total+=a[2].precio;
				  a[2].unidades++;
			break;
			
			case 'd': case'D':
				  total+=a[3].precio;
				  a[3].unidades++;
	        break;
	        default:
			break;
	       }//Con este switch se le van añadiendo las unidades pedidas para cada torta, asi como para el total.
			
			p("Tu orden al momento es: \n");	       
	        p(" %d Cubana   \n", a[0].unidades);
			p(" %d Jamon    \n", a[1].unidades); 
	    	p(" %d Especial \n", a[2].unidades); 
			p(" %d Refresco \n", a[3].unidades);  
	       	p("\n Total es de: %d\n\n", total);
	      
	}while(opcion);
	
}

int menu (int res)
{
	
	printf("\tMenu\n\n");
	printf("a.- Torta cubana   - $40\n");
	printf("b.- Torta de jamon - $15\n");
	printf("c.- Torta especial - $55\n");
	printf("d.- Refresco       - $10\n");
	printf("e.- Terminar orden y salirse\n");	
	printf("\nIngrese una opcion: ");
	fflush(stdin);  
    res=getchar();
	return res;

}//Esta funcion nos sirve para mostrar el menu cada vez que sea llamada y guardar la opcion que eligio el usuario
