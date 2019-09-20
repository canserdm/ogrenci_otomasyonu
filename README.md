# ogrenci_otomasyonu

#include<iostream>
#include<cmath>
#include<conio.h>
#include<fstream>
#include<string.h>
#include <sstream>
using namespace std;
int main(){
	int secim,sayac=0,sinif,k=0,l=0;
	string ad,soyad,bolum,dizi[100][100],ogr_no,notu;
	string ogrt_ad,ogrt_soyad,ogrt_bolum,ders_ad,satir,no,ders,blm;
	char secim2;
	ofstream yazma;					//Input stream
	ifstream okuma;					//Output stream
	
	baslangic:
	system("cls");													//ana menü
	cout<<"\n-----------MODULLER-----------"<<endl;
	cout<<" 1. Ogrenci Modulu"<<endl;
	cout<<" 2. Ogretim Elemani Modulu"<<endl;
	cout<<" 3. Ders Modulu"<<endl;
	cout<<" 4. Not Giris Modulu"<<endl;
	cout<<" 5. Cikis"<<endl;
	cout<<"------------------------------"<<endl;
	cout<<"\nModul Seciniz: ";									//islem yapilacak modulun secimi yapılıyor
	cin>>secim;
	switch(secim){
		case 1: goto ogr_mdl;					//ana menuden ogrenci modulune gönderiliyor
		case 2: goto ogr_el_mdl;				//ana menuden ogretim elemanı modulune gönderiliyor
		case 3: goto ders_mdl;					//ana menuden ders modulune gönderiliyor
		case 4: goto not_grs_mdl;				//ana menuden not girisi modulune gönderiliyor
		case 5: goto cikis;
	}
	ogr_mdl:
		don:
		system("cls");
		cout<<"\n-----------OGRENCI MODULU---------"<<endl;		//Ogrenci modulunde yapılmak istenen islemler menu halinde olusturuluyor
		cout<<" 1. Ogrenci Kayit"<<endl;
		cout<<" 2. Ogrenci Arama"<<endl;
		cout<<" 3. Ogrenci Listeleme"<<endl;
		cout<<" 4. Ana Menuye Don"<<endl;
		cout<<"----------------------------------"<<endl;
		cout<<"\nYapmak istediginiz islemi seciniz: ";					//ogrenci modulunde yapilmak istenen islem seciliyor
		cin>>secim;
		
		switch(secim){
			case 4:	goto baslangic;
			case 1:	
				kayit:							
				system("cls");
				cout<<"\n---------Ogrenci Kayit---------";
				yazma.open("ogrenci.txt",ios::app);							//ogrenci adinda dosya olusturuluyor
				
				if(!yazma.is_open()){
					cerr<<"Dosya Bulunamadi!!!"<<endl;
					abort();
				}
				
				cout<<"\nOgrencinin Numarasi: ";	cin>>ogr_no;		//ogrencinin bilgileri kullanıcı tarafından giriliyor
				cout<<"Adi: ";	cin>>ad;
				cout<<"Soyadi: ";	cin>>soyad;
				cout<<"Bolum: ";	cin>>bolum;
				cout<<"Sinifi: ";	cin>>sinif;
				
				yazma<<"\n"<<ogr_no;					//Ogrenci bilgileri dosyaya yazdırılıyor
				yazma<<"\t"<<ad;  
				yazma<<"\t"<<soyad;
				yazma<<"\t"<<bolum;
				yazma<<"\t"<<sinif;
				cout<<"Kayit yapilmistir.";
				
				yazma.close();				//dosya kapatiliyor
				tekrar:																
				cout<<"\nbaska kayit yapmak ister misiniz?(e/h): ";				
				cin>>secim2;
				if(secim2=='e'||secim2=='E')	goto kayit;						//tekrar kayit yapilmak istendiğinde kayit etiketinin olduğu satirdan devam ediyor
					else if(secim2=='h'||secim2=='H')	goto don;			//kayit yapilmak istenmediğinde ana menuye donuyor
						else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
							cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
							goto tekrar;
						}
				
				
			case 2:
				arama:
				system("cls");
				cout<<"\n---------Ogrenci Arama---------";
				cout<<"\n1.Ogrenci numarasina gore arama";
				cout<<"\n2.Ogrenci adina gore arama";
				cout<<"\n-------------------------------";
				cout<<"\nArama Kriterini Seciniz:";
				cin>>secim;
				while(secim==1){
					string numara;
    				string satir;
    						
    				okuma.open("ogrenci.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
					sayac=0;
    				cout<<"Aramak istediginiz numarayi girin :";
    				cin>>numara;
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<5;l++){
							if(numara==dizi[k][l]){
								cout<<"->";
								for(l=0;l<5;l++){
									sayac++;
									cout<<" "<<dizi[k][l];
								}
								cout<<endl;
							}
						}
						l=0;
						k++;		
							
					}
					if(sayac==0)	cout<<"aranilan numara bulunamadi";	
					okuma.close();
					tekrar1:																
					cout<<"\ntekrar arama yapmak ister misiniz?(e/h): ";				
					cin>>secim2;
					if(secim2=='e'||secim2=='E')	goto arama;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
						else if(secim2=='h'||secim2=='H')	goto don;			//arama yapilmak istenmediğinde ana menuye donuyor
							else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
								cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
								goto tekrar1;
							}
				}
				
				
				while(secim==2){
					string isim;
    				string satir;
    						
    				okuma.open("ogrenci.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
					
    				cout<<"Aramak istediginiz ismi girin :";
    				cin>>isim;
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<5;l++){
							if(isim==dizi[k][l]){
								cout<<"->";
								for(l=0;l<5;l++){
									sayac++;
									cout<<" "<<dizi[k][l];
								}
								cout<<endl;
							}
						}
						l=0;
						k++;
					}
					if(sayac==0)	cout<<"aranilan isim bulunamadi";
					okuma.close();
					tekrar2:																
					cout<<"\ntekrar arama yapmak ister misiniz?(e/h): ";				
					cin>>secim2;
					if(secim2=='e'||secim2=='E')	goto arama;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
						else if(secim2=='h'||secim2=='H')	goto don;			//arama yapilmak istenmediğinde ana menuye donuyor
							else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
								cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
								goto tekrar2;
							}
					
				}
				while(secim!=1&&!secim2){
					cout<<"\a Yanlis secim yaptiniz!"<<endl;
					system("pause");
					goto arama;
				}	
				okuma.close();
			case 3:	
				listele:
				system("cls");
				cout<<"\n---------Ogrenci listeleme---------";
				cout<<"\n1.Bolume gore listeleme";
				cout<<"\n2.Sinifa gore listeleme";
				cout<<"\n-------------------------------";
				cout<<"\nListeleme Kriterini Seciniz:";
				cin>>secim;			
				while(secim==1){
					string blm;
    				string satir;
    						
    				okuma.open("ogrenci.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
					sayac=0;
    				cout<<"Listelemek istediginiz bolumu giriniz :";
    				cin>>blm;
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<5;l++){
							if(blm==dizi[k][l]){
								cout<<"->";
								for(l=0;l<5;l++){
									sayac++;
									cout<<" "<<dizi[k][l];
								}
								cout<<endl;
							}
						}
						l=0;
						k++;		
							
					}
					if(sayac==0)	cout<<"Listelenmek istenen bolum dosyanizda bulunmamaktadir.";	
					okuma.close();
					tekrar3:																
					cout<<"\nTekrar arama yapmak ister misiniz?(e/h): ";				
					cin>>secim2;
					if(secim2=='e'||secim2=='E')	goto listele;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
						else if(secim2=='h'||secim2=='H')	goto don;			//arama yapilmak istenmediğinde ana menuye donuyor
							else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
								cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
								goto tekrar3;
							}
				}
				while(secim==2){
					string snf;
    				string satir;
    						
    				okuma.open("ogrenci.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
					sayac=0;
    				cout<<"Listelemek istediginiz sinifi giriniz :";
    				cin>>snf;
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<5;l++){
							if(snf==dizi[k][l]){
								cout<<"->";
								for(l=0;l<5;l++){
									sayac++;
									cout<<" "<<dizi[k][l];
								}
								cout<<endl;
							}
						}
						l=0;
						k++;		
							
					}
					if(sayac==0)	cout<<"Listelenmek istenen sinifa ait ogrenci dosyanizda bulunmamaktadir.";	
					okuma.close();
					tekrar4:																
					cout<<"\nTekrar listeleme yapmak ister misiniz?(e/h): ";				
					cin>>secim2;
					if(secim2=='e'||secim2=='E')	goto listele;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
						else if(secim2=='h'||secim2=='H')	goto don;			//arama yapilmak istenmediğinde ana menuye donuyor
							else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
								cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
								goto tekrar4;
							}
				}
				while(secim!=1&&!secim2){
					cout<<"\a Yanlis secim yaptiniz!"<<endl;
					system("pause");
					goto listele;
				}	
				
			default:{goto don;
				break;
			} 
							
		}
	
	ogr_el_mdl:	
		don2:
		system("cls");
		cout<<"\n-----------OGRETIM ELEMANI MODULU---------"<<endl;		//Ogretim elemani modulunde yapılmak istenen islemler menu halinde olusturuluyor
		cout<<" 1. Ogretim Elemani Kayit"<<endl;
		cout<<" 2. Ogretim Elemani Arama(Sicil numarasina gore)"<<endl;
		cout<<" 3. Ogretim Elemani Listeleme(Bolume gore)"<<endl;
		cout<<" 4. Ana Menuye Don"<<endl;
		cout<<"----------------------------------"<<endl;
		cout<<"\nYapmak istediginiz islemi seciniz: ";					//ogretim elemanı modulunde yapilmak istenen islem seciliyor
		cin>>secim;
		switch(secim){
			case 4:	goto baslangic;
			case 1:	
				int sicil_no;
				kayit2:							
				system("cls");
				cout<<"\n---------Ogretim elemani Kayit---------";
				yazma.open("ogretim_elemani.txt",ios::app);							//ogrenci adinda dosya olusturuluyor
				if(!yazma.is_open()){
					cerr<<"Dosya Bulunamadi!!!"<<endl;
					abort();
				}
				
				cout<<"\nsicil numarasi: ";	cin>>sicil_no;		//ogrencinin bilgileri kullanıcı tarafından giriliyor
				cout<<"Adi: ";	cin>>ogrt_ad;
				cout<<"Soyadi: ";	cin>>ogrt_soyad;
				cout<<"Bolum: ";	cin>>ogrt_bolum;
				
				yazma<<"\n"<<sicil_no;					//Ogrenci bilgileri dosyaya yazdırılıyor
				yazma<<"\t"<<ogrt_ad;  
				yazma<<"\t"<<ogrt_soyad;
				yazma<<"\t"<<ogrt_bolum;
				cout<<"Kayit yapilmistir.";
				
				yazma.close();				//dosya kapatiliyor
				tekrar5:																
				cout<<"\nbaska kayit yapmak ister misiniz?(e/h): ";				
				cin>>secim2;
				if(secim2=='e'||secim2=='E')	goto kayit2;						//tekrar kayit yapilmak istendiğinde kayit etiketinin olduğu satirdan devam ediyor
					else if(secim2=='h'||secim2=='H')	goto don2;			//kayit yapilmak istenmediğinde ana menuye donuyor
						else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
							cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
							goto tekrar5;
						}
				
				
			case 2:
    				arama2:
    						
    				okuma.open("ogretim_elemani.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
					sayac=0;
					system("cls");
    				cout<<"\n Aramak istediginiz sicil numarasini giriniz :";
    				cin>>no;
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<5;l++){
							if(no==dizi[k][l]){
								
								cout<<"->";
								for(l=0;l<5;l++){
									sayac++;
									cout<<" "<<dizi[k][l];
								}
								cout<<endl;
							}
						}
						l=0;
						k++;
					}
					if(sayac==0)	cout<<"aranilan sicil numarasi bulunamadi";
					okuma.close();	
					tekrar6:																
					cout<<"\ntekrar arama yapmak ister misiniz?(e/h): ";				
					cin>>secim2;
					if(secim2=='e'||secim2=='E')	goto arama2;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
						else if(secim2=='h'||secim2=='H')	goto don2;			//arama yapilmak istenmediğinde ana menuye donuyor
							else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
								cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
								goto tekrar6;
							}	
					break;
			case 3:
				listele1:
				system("cls");
				cout<<"\n---------Ogretim Elemani listeleme---------"<<endl;
					
    				okuma.open("ogretim_elemani.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
					sayac=0;
    				cout<<"Listelemek istediginiz bolumu giriniz :";
    				cin>>blm;
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<5;l++){
							if(blm==dizi[k][l]){
								cout<<"->";
								for(l=0;l<5;l++){
									sayac++;
									cout<<" "<<dizi[k][l];
								}
								cout<<endl;
							}
						}
						l=0;
						k++;		
							
					}
					if(sayac==0)	cout<<"Listelenmek istenen bolum dosyanizda bulunmamaktadir.";	
					okuma.close();
					tekrar7:																
					cout<<"\nTekrar listeleme yapmak ister misiniz?(e/h): ";				
					cin>>secim2;
					if(secim2=='e'||secim2=='E')	goto listele1;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
						else if(secim2=='h'||secim2=='H')	goto don2;			//arama yapilmak istenmediğinde ana menuye donuyor
							else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
								cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
								goto tekrar7;
							}
			default:{goto don2;
				break;
			} 																	
		}	
		
		
		
		
		
		
		
	ders_mdl:	
		don3:
		system("cls");
		cout<<"\n-----------DERS MODULU---------"<<endl;		//Ogrenci modulunde yapılmak istenen islemler menu halinde olusturuluyor
		cout<<" 1. Ders Ekleme"<<endl;
		cout<<" 2. Ders Arama (Ders adina gore)"<<endl;
		cout<<" 3. Ders Listeleme"<<endl;
		cout<<" 4. Ana Menuye Don"<<endl;
		cout<<"----------------------------------"<<endl;
		cout<<"\nYapmak istediginiz islemi seciniz: ";					//ogrenci modulunde yapilmak istenen islem seciliyor
		cin>>secim;	
		switch(secim){
			case 4:	goto baslangic;
			case 1:	
				int kod;
				kayit9:						
				system("cls");
				cout<<"\n---------Ders Ekleme---------";
				yazma.open("ders.txt",ios::app);							//ogrenci adinda dosya olusturuluyor
				if(!yazma.is_open()){
					cerr<<"Dosya Bulunamadi!!!"<<endl;
					abort();
				}
				
				cout<<"\nDers kodu: ";	cin>>kod;		//ogrencinin bilgileri kullanıcı tarafından giriliyor
				cout<<"Dersin adi: ";	cin>>ders_ad;
				
				yazma<<"\n"<<kod;					//Ogrenci bilgileri dosyaya yazdırılıyor
				yazma<<"\t"<<ders_ad;
				cout<<"Kayit yapilmistir.";
				
				yazma.close();				//dosya kapatiliyor
				tekrar9:																
				cout<<"\nbaska ders eklemek ister misiniz?(e/h): ";				
				cin>>secim2;
				if(secim2=='e'||secim2=='E')	goto kayit9;						//tekrar kayit yapilmak istendiğinde kayit etiketinin olduğu satirdan devam ediyor
					else if(secim2=='h'||secim2=='H')	goto don3;			//kayit yapilmak istenmediğinde ana menuye donuyor
						else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
							cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
							goto tekrar9;
						}
			
			case 2:
    				arama3:
    						
    				okuma.open("ders.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
					sayac=0;
					system("cls");
    				cout<<"\n Aramak istediginiz dersin adini giriniz :";
    				cin>>ders;
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<2;l++){
							if(ders==dizi[k][l]){
								
								cout<<"->";
								for(l=0;l<2;l++){
									sayac++;
									cout<<" "<<dizi[k][l];
								}
								cout<<endl;
							}
						}
						l=0;
						k++;	
							
					}
					if(sayac==0)	cout<<"aranilan ders bulunamadi";
					okuma.close();	
					tekrar10:																
					cout<<"\ntekrar arama yapmak ister misiniz?(e/h): ";				
					cin>>secim2;
					if(secim2=='e'||secim2=='E')	goto arama3;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
						else if(secim2=='h'||secim2=='H')	goto don3;			//arama yapilmak istenmediğinde ana menuye donuyor
							else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
								cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
								goto tekrar10;
							}	
							
			case 3:
				listele2:
				system("cls");
				cout<<"\n---------Ders listeleme---------"<<endl;
					
    				okuma.open("ders.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
					sayac=0;
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<3;l++){
							cout<<"->";
							for(l=0;l<3;l++){
								sayac++;
								cout<<" "<<dizi[k][l];
							}
							cout<<endl;
						}
						l=0;
						k++;		
							
					}
					if(sayac==0)	cout<<"Dosyanizda ders bulunmamaktadir.";	
					okuma.close();
					system("pause");
					goto don3;	
					
			default:{goto don3;
				break;
			} 											
		}
	
	not_grs_mdl:
		don4:
		system("cls");
		cout<<"\n-----------NOT GIRIS MODULU---------"<<endl;		//Ogrenci modulunde yapılmak istenen islemler menu halinde olusturuluyor
		cout<<" 1. Ogrenciye Ders Ekleme"<<endl;
		cout<<" 2. Ogrencinin Aldigi Ders Icin Not Girisi"<<endl;
		cout<<" 3. Ogrenci Ders Listeleme"<<endl;
		cout<<" 4. Ogrenci Karnesi Olusturma ve Gorsellestirme"<<endl;
		cout<<" 5. Ana Menuye Don"<<endl;
		cout<<"----------------------------------"<<endl;
		cout<<"\nYapmak istediginiz islemi seciniz: ";					//ogrenci modulunde yapilmak istenen islem seciliyor
		cin>>secim;	
		switch(secim){
			case 5:	goto baslangic;
			case 1:
				
				yazma.open("ders_ekleme.txt",ios::app);
				if(!yazma.is_open()){
					cerr<<"Dosya Bulunamadi!!!"<<endl;
					abort();
				}
				okuma.open("ogrenci.txt",ios::app);							//ogrenci adinda dosya olusturuluyor
				if(!okuma.is_open()){
					cerr<<"Dosya Bulunamadi!!!"<<endl;
					abort();
				}
				gir:
				no=" ";
				system("cls");
				cout<<"\n Ders eklemek istediginiz ogrencinin numarasini giriniz: ";
				cin >>no;
				
				
   				cout<<"\n\t******"<<endl;
				sayac=0;
   				while(!okuma.eof()){
    				getline(okuma,satir);
					istringstream row(satir);
					for(int i=0;row;i++){
						string str;
						row>>str;
						dizi[k][l]=str;
						l++;
					}
					for(l=0;l<4;l++){
						if(no==dizi[k][l]){
							sayac++;
							yazma<<"\n "<<dizi[k][l]<<" "<<dizi[k][l+1]<<" "<<dizi[k][l+2];
							goto ders_gir;
						}
					}
					l=0;
					k++;
				}
					if(sayac==0)	{
						cout<<"Girdiginiz numarada ogrenci bulunmamaktadir.\nTekrar deneyin!"<<endl;
						system("pause");
						goto gir;	
					}
					while(!okuma.eof()){
					for(l=0;l<4;l++){
						if(no==dizi[k][l]){
							ders_gir:
							system("cls");
							cout<<"->";
							for(l=0;l<4;l++){
								sayac++;
								cout<<" "<<dizi[k][0]<<" "<<dizi[k][1]<<" "<<dizi[k][2];
								cout<<"\nOgrenciye eklemek istediginiz dersin adini giriniz: ";
								cin>>ders;
								yazma<<"\t"<<ders;
								tekrar13:
								system("cls");	
								cout<<" "<<dizi[k][0]<<" "<<dizi[k][1]<<" "<<dizi[k][2]<<endl;													
								cout<<"\nTekrar ders eklemek ister misiniz?(e/h): ";				
								cin>>secim2;
								if(secim2=='e'||secim2=='E')	goto gir;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
									else if(secim2=='h'||secim2=='H')	goto don4;			//arama yapilmak istenmediğinde ana menuye donuyor
										else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
											cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
											goto tekrar13;
										}	
							}
						}
						l=0;
						k++;
					}
				
					okuma.close();
					yazma.close();
				}
			case 2:
				yazma.open("notlar.txt",ios::app);
				if(!yazma.is_open()){
					cerr<<"Dosya Bulunamadi!!!"<<endl;
					abort();
				}
				okuma.open("ders_ekleme.txt",ios::app);							//ogrenci adinda dosya olusturuluyor
				if(!okuma.is_open()){
					cerr<<"Dosya Bulunamadi!!!"<<endl;
					abort();
				}
				
				gir2:
					no=" ";
				system("cls");
				cout<<"\n Ders notunu eklemek istediginiz ogrencinin numarasini giriniz: ";
				cin >>no;
				
   				cout<<"\n\t******"<<endl;
				sayac=0;
				k=-1;
   				while(!okuma.eof()){
   					not_gir:
					l=0;
					k++;
    				getline(okuma,satir);
					istringstream row(satir);
					for(int i=0;row;i++){
						string str;
						row>>str;
						dizi[k][l]=str;
						l++;
					}
					for(l=0;l<4;l++){
						if(no==dizi[k][l]){
							sayac++;
							yazma<<"\n "<<dizi[k][l]<<" "<<dizi[k][l+1]<<" "<<dizi[k][l+2]<<" "<<dizi[k][l+3]<<": ";
							goto dersnotu_gir;
						}
					}
				}
					if(sayac==0)	{
						cout<<"Girdiginiz numarada ogrenci bulunmamaktadir.\nTekrar deneyin!"<<endl;
						system("pause");
						goto gir2;	
					}
					while(!okuma.eof()){
					for(l=0;l<4;l++){
						if(no==dizi[k][l]){
							
							dersnotu_gir:
							system("cls");
							cout<<"->";
							for(l=0;l<4;l++){
								sayac++;
								cout<<" "<<dizi[k][0]<<" "<<dizi[k][1]<<" "<<dizi[k][2]<<" "<<dizi[k][4];
								cout<<"\nOgrencinin notunu giriniz: ";
								cin>>notu;
								yazma<<notu;
								if(!okuma.eof())	goto not_gir;
								tekrar14:
								system("cls");	
								cout<<" "<<dizi[k][0]<<" "<<dizi[k][1]<<" "<<dizi[k][2]<<endl;													
								cout<<"\nTekrar not girisi yapmak ister misiniz?(e/h): ";				
								cin>>secim2;
								if(secim2=='e'||secim2=='E')	goto gir2;						//tekrar arama yapilmak istendiğinde arama etiketinin olduğu satirdan devam ediyor
									else if(secim2=='h'||secim2=='H')	goto don4;			//arama yapilmak istenmediğinde ana menuye donuyor
										else {															//yanlis secim yapildiginda tekrar secim yaptiriliyor
											cout<<"\a\tYanlis secim yaptiniz!\n\tLutfen tekrar deneyin!" ;   
											goto tekrar14;
										}
								goto not_gir;
									
							}
						}
						l=0;
						k++;
					}
				
					okuma.close();
					yazma.close();
				}	
				
			case 3:
				system("cls");
				cout<<"\n---------Ogrenci Ders listeleme---------"<<endl;
					
    				okuma.open("ders_ekleme.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
   					cout<<"\n\t******"<<endl;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						for(l=0;l<5;l++){
							cout<<"->";
							for(l=0;l<5;l++){
								sayac++;
								cout<<" "<<dizi[k][l];
							}
							cout<<endl;
						}
						l=0;
						k++;		
							
					}
					if(sayac==0)	cout<<"Dosyanizda ders bulunmamaktadir.";	
					okuma.close();
					system("pause");
					goto don4;	
					
			case 4:	
				system("cls");
				cout<<"\n---------Ogrenci Karnesi---------"<<endl;
					
    				okuma.open("notlar.txt",ios::app);//arama yapılacak dosya ismi
    				if(!okuma.is_open()){
						cerr << "HATA: BOYLE BIR DOSYA MEVCUT DEGIL!" << endl;   
      					abort();
					}
   					cout<<"Karnesini goruntulemek istediginiz ogrencinin numarasini giriniz: "<<endl;
   					cin>>no;
   					while(!okuma.eof())
    				{	int k=0,l=0;
    					getline(okuma,satir);
						istringstream row(satir);
						for(int i=0;row;i++){
							string str;
							row>>str;
							dizi[k][l]=str;
							l++;
						}
						if(no==dizi[k][0]){
							for(l=0;l<6;l++){
								cout<<"***********"<<endl;
								for(l=0;l<6;l++){
									sayac++;
									if(l==0)	cout<<"Ogrencinin Numarasi: ";
									else if(l==1)	cout<<"Ogrencinin Adi: ";
									else if(l==2)	cout<<"Ogrencinin Soyadi: ";
									else if(l==3)	cout<<"Ogrencinin Bolumu: ";
									else if(l==4)	cout<<"Ogrencinin Dersi: ";
									else cout<<"Ogrencinin Notu: ";
									cout<<dizi[k][l]<<endl;
								}
								cout<<endl;
							}
						}
						l=0;
						k++;		
							
					}
					if(sayac==0)	cout<<"Dosyanizda ders bulunmamaktadir.";	
					okuma.close();
					system("pause");
					goto don4;	
			default:{goto don4;
				break;
			} 			
		} 
	cikis:					
	return 0;
}
