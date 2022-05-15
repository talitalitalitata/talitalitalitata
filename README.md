#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<windows.h>
#include <MMsystem.h>


void d_ujek();
void jastip();
void ujek();
void emoney();
void edmoney();
void driver_int();
void ujek();
void driver();
void registrasi();
void login();
void user_int();
void converter();
char aj[50],aa[50];
	struct checker{
		char name[50],pw[50],clas[50],status[50];
	}ch[100];
	FILE *user;
	FILE *tem;
int i,jb,bb;
char usr[50], pas[50];
struct user{
	char clas[50],nama[50],alamat[50],status[50];
	int hp,saldo;
	char username[50],password [50];
	char alamatjemput[100],alamatantar[100];
    int jumlah,berat,nominal;
}data;

main(){
	
	int pilihan;
	converter();
   printf ("Welcome to U-JEK!\n");
   printf ("\n");
   printf ("1. Registrasi\n2. Login\n");
   printf ("\n");
   printf ("Pilih Registrasi jika belum memiliki akun atau login jika sudah memiliki\n");
   printf ("Pilihan : ");
   scanf  ("%d", &pilihan); getchar();
   system("cls");

   switch (pilihan){
   case 1 : registrasi(); break;
   case 2 : login(); break;
   case 10 : system("cls");
   printf ("user detail\n\n");
   user=fopen("user.dat","rb");
	while(fread(&data,sizeof(data),1,user)==1){
		printf ("Name : %s\n",data.nama);
		printf ("clas : %s \n", data.clas);
		printf ("alamat : %s \n",data.alamat);
		printf ("status : %s \n",data.status);
		printf ("no hp : %d \n",data.hp);
		printf ("saldo : %d \n",data.saldo);
		printf ("username : %s \n",data.username);
		printf ("password : %s \n",data.password);
		printf ("alamat jemput : %s \n",data.alamatjemput);
		printf ("alamat antar : %s \n",data.alamatantar);
		printf ("jumlah barang : %d \n",data.jumlah);
		printf ("berat : %d \n",data.berat);
		printf ("nominal : %d \n\n",data.nominal);
	}main();break;
   }
}

void login(){
 
   
	fflush(stdin);
	converter();
	int j;
	for (j=0;j<3;j++){
      printf("Masukkan Username : ");
      gets(usr);
      printf("Masukkan Password : ");
      gets(pas);
	
	for(i=0;i<100;i++){
		if((strcmp(ch[i].name,usr)==0)&&(strcmp(ch[i].pw,pas)==0))
		{if (strcmp(ch[i].clas,"user")==0){
			
		system("cls");
			user_int();}
			else if (strcmp(ch[i].clas,"driver")==0){
			system("cls");
			driver_int();}
		}
		
	}
	  system ("cls");
         printf("Username dan Password tidak match\n");
		 }
        main();
         

   

   
}

void registrasi(){
	int i, pilreg;
	converter();
	printf ("\n");
	printf ("Registrasi Akun U_JEK\n");
	printf("\nDaftar Sebagai\n");
	printf("\n1. User\n2. Driver\n");
	printf ("Pilihan : ");
	user = fopen("user.dat","ab");
	scanf("%d", &pilreg);getchar();
	switch(pilreg){
		case 1 : strcpy(data.clas,"user");strcpy(data.status,"NA");break;
		case 2 :strcpy(data.clas,"driver");
		strcpy(data.status,"NA");break;
		default : 	system("cls");
		printf("PILIHAN TIDAK TERSEDIA !\n");
		registrasi();break;
	}

	system("cls");
	printf ("\n");
	
	printf ("Buat Username dan Password\n");
	printf ("Username      : ");
		scanf ("%s", &data.username);
		for (i=0;i<=100;i++){
			if (strcmp(ch[i].name,data.username)==0)
			{
				printf ("Username telah terpakai !");
				registrasi();
			}
		}
	printf ("Password      : ");
		scanf ("%s", &data.password);getchar();
	printf ("\n");
	printf ("Masukan Biodata Diri Anda!\n");
	printf ("Nama          : ");
		gets(data.nama);
	printf ("Alamat        : ");
		gets(data.alamat);
	printf ("No HP         : ");
		scanf ("%d", &data.hp);getchar();
	
	fwrite(&data, sizeof(data), 1, user);
	fflush(stdin);
	fclose(user);
	system("cls");
	printf("data tersimpan !\n\n");
	main();
}



void converter(){
	
	i=0;
	user = fopen("user.dat","rb");
		while(fread(&data,sizeof(data),1,user)==1){
			strcpy(ch[i].name,data.username);
			strcpy(ch[i].pw,data.password);
			strcpy(ch[i].clas,data.clas);
			strcpy(ch[i].status,data.status);
			i=i+1;
		}
	fclose(user);
}

void user_int(){
int menu,bs;
    
    printf ("Menu Pengguna\n\n");
 printf ("1. U-Jek (Jasa ojek online)\n");
 printf ("2. U-Send (Jasa antar barang)\n");
 printf ("3. U-Money (Top-up Uang)\n");
 printf ("4. Log-Out\n");
 printf ("\nPilih Menu : ");scanf("%d",&menu);fflush(stdin);system("cls");

 switch (menu){
 	case 1: system("cls");
	 if (strcmp(ch[i].status,"NA")==0)
	 ujek();
	 else {printf ("Harap tunggu orderan sebelumnya :)\n");
		user_int();
	
}
	 break;
    case 2: 
	 if (strcmp(ch[i].status,"NA")==0)
	 jastip();
	 else {printf ("Harap tunggu orderan sebelumnya :)\n");
		user_int();
		
    system("cls");break;
    case 3: emoney();break;
    case 4: main();break;
    default : system("cls");
	printf ("Menu tidak tersedia !!!\n");
	user_int();
    }
	}}
    
    void ujek(){
	
    printf("\nPemesan ojek online\n");
    printf("Masukkan alamat penjemputan anda!\n");
    printf("Alamat  : ");gets(aj);
    printf("Masukkan alamat tujuan  anda!\n");
    printf("Alamat  : ");gets(aa);
    
    user=fopen("user.dat","rb");
 	tem=fopen("tem.dat","wb");
 	while(fread(&data,sizeof(data),1,user)==1){
 		if(strcmp(data.username,usr)==0){
 		strcpy(data.status,"order ojek");
 		strcpy(data.alamatantar,aa);
 		strcpy(data.alamatjemput,aj);
		 }
		 fwrite(&data,sizeof(data),1,tem);
	 }
	 fclose(user);
	 fclose(tem);
	 remove("user.dat");
	 rename("tem.dat","user.dat");
	system("cls");
	printf ("harap tunggu :)\n\n");
	user_int();
    //mencari driver dan dapat driver
    //fitur chat muncul
    //mulai perjalanan
    //selesai orderan
    //rating driver--selesai---
    
}   


void jastip(){
    printf("\nPemesan ojek online\n");
    printf("Masukkan alamat penjemputan barang anda!\n");
    printf("Alamat  : ");gets(aj);
    printf("Masukkan alamat tujuan pengantaran barang anda!\n");
    printf("Alamat  : ");gets(aa);
    printf("Masukkan jumlah dan berat barang\n");
    printf("Jumlah  : ");scanf("%d",jb);getchar();
    printf("Berat : ");scanf("%d",&bb);getchar();
    
    user=fopen("user.dat","rb");
 	tem=fopen("tem.dat","wb");
 	while(fread(&data,sizeof(data),1,user)==1){
 		if(strcmp(data.username,usr)==0){
 		strcpy(data.status,"order kurir");
 		strcpy(data.alamatantar,aa);
 		strcpy(data.alamatjemput,aj);
 		data.berat=bb;
 		data.jumlah=jb;
		 }
		 fwrite(&data,sizeof(data),1,tem);
	 }
	 fclose(user);
	 fclose(tem);
	 remove("user.dat");
	 rename("tem.dat","user.dat");

	system("cls");
	printf ("harap tunggu :)\n\n");
	user_int();
    //mencari driver dan dapat driver
    //fitur chat muncul
    //mulai perjalanan
    //selesai orderan
    //rating driver--selesai---
}

void emoney(){
    int duit,cek,menum;
    printf ("1. Top Up\n");
    printf ("2. Cek Saldo\n");
    printf ("3. Back\n");
    printf ("\nPilih Menu : ");scanf("%d",&menum);fflush(stdin);
    switch (menum){
    case 1: system("cls"); 
	printf("Top UP\n");
    printf("Masukkan Masukkan banyak nominal top up anda!\n");
    printf("Nominal  : ");scanf("%d",&duit);getchar();
    user=fopen("user.dat","rb");
 	tem=fopen("tem.dat","wb");
 	while(fread(&data,sizeof(data),1,user)==1){
 		if(strcmp(data.username,usr)==0){
 			data.saldo=data.saldo+duit;
		 }
		 fwrite(&data,sizeof(data),1,tem);
	 }
	 fclose(user);
	 fclose(tem);
	 remove("user.dat");
	 rename("tem.dat","user.dat");
	 system("cls");
	 printf ("uang berhasil di topup! :)\n\n");
	 user_int();break;
    case 2: system("cls");printf("Cek Saldo\n");
    printf("%c",data.nominal);
		
		user=fopen("user.dat","rb");
 	 	while(fread(&data,sizeof(data),1,user)==1)
 		if(strcmp(data.username,usr)==0){
 		printf ("Saldo anda : Rp. %d\n\n",data.saldo);
	 }
	 fclose(user);
	system("pause");
	system("cls");
	user_int();break;
	case 3 : system("cls");
	user_int();
    default : 
	printf ("Pilihan tidak tersedia !!!\n\n");
    user_int();
	break;
	
	}}
	
void driver_int(){
	 int md,bs;
	 
	 	int kurir,ojek;
	
	 user=fopen("user.dat","rb");
	 while(fread(&data,sizeof(data),1,user)==1){
	 if(strcmp(data.status,"order kurir")==0){
	 kurir=kurir+1;}
	 else if (strcmp(data.status,"order ojek")==0){
	 ojek=ojek+1;}
}fclose(user);
if((kurir>0)||(ojek>0)){
		//PlaySound (TEXT("Untitled.wav"),NULL,SND_ASYNC); 
		//MessageBox(0,"Ada Orderan :) ","Notification",1);
}

    printf ("Menu Driver\n\n");
 printf ("1. U-Jek (Mengambil order)\n");
 printf ("2. U-Saldo (Jumlah Total Uang)\n");
 printf ("3. U-Orderan Selesai (Jumlah Orderan Selesai)\n"	);
 printf ("4. U- Rating \n");
 printf ("\nPilih Menu : ");scanf("%d",&md);getchar();

 switch (md){
    case 1 : d_ujek(); break;
    case 2 : edmoney(); break;
    //case 3: saldo();break;
    //case 4: orderan();break;
    //case 5: rating();break;
    //case 6: chat();break;
    
}

}

void edmoney(){
    int duit,cek,menum;
    system("cls");
    printf ("1. Top Up\n");
    printf ("2. Cek Saldo\n");
    printf ("3. Back\n");
    printf ("\nPilih Menu : ");scanf("%d",&menum);fflush(stdin);
    switch (menum){
    case 1: system("cls"); 
	printf("Top UP\n");
    printf("Masukkan Masukkan banyak nominal top up anda!\n");
    printf("Nominal  : ");scanf("%d",&duit);getchar();
    user=fopen("user.dat","rb");
 	tem=fopen("tem.dat","wb");
 	while(fread(&data,sizeof(data),1,user)==1){
 		if(strcmp(data.username,usr)==0){
 			data.saldo=data.saldo+duit;
		 }
		 fwrite(&data,sizeof(data),1,tem);
	 }
	 fclose(user);
	 fclose(tem);
	 remove("user.dat");
	 rename("tem.dat","user.dat");
	 system("cls");
	 printf ("uang berhasil di topup! :)\n\n");
	 driver_int();break;
    case 2: system("cls");printf("Cek Saldo\n");
    printf("%c",data.nominal);
		
		user=fopen("user.dat","rb");
 	 	while(fread(&data,sizeof(data),1,user)==1)
 		if(strcmp(data.username,usr)==0){
 		printf ("Saldo anda : Rp. %d\n\n",data.saldo);
	 }
	 fclose(user);
	system("pause");
	system("cls");
	driver_int();break;
	case 3 : system("cls");
	user_int();
    default : 
	printf ("Pilihan tidak tersedia !!!\n\n");
    driver_int();
	break;
	
	}}
	
	void d_ujek(){
	
		i=0;
		printf ("===List Order===\n\n");
		user=fopen("user.dat","rb");
		while(fread(&data,sizeof(data),1,user)==1){
			if (strcmp(data.status,"order ojek")==0){
				printf ("U-jek\n");
				printf ("%d Nama : %s\n",i,data.nama);
				printf ("Lokasi Jemput : %s \n", data.alamatjemput);
				printf ("Lokasi Antar : %s \n",data.alamatantar);
			}
			else if(strcmp(data.status,"order kurir")==0){
				printf ("Jastip \n");
				printf ("%d Nama : %s\n",i,data.nama);
				printf ("Lokasi Pickup : %s \n", data.alamatjemput);
				printf ("Lokasi Antar : %s \n",data.alamatantar);
			}
			
			i=i+1;
		}
		
		
	}
