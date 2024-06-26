#include <Arduino.h>

int i;

int extg = 36 ; //initialisation capteur CNY70
int intg = 39 ; //initialisation capteur CNY70
int extd= 35 ; //initialisation capteur CNY70
int intd = 34 ; //initialisation capteur CNY70
int resolution =10; // pour le servo moteur 
//int encodeur = ; //initialisation de l'encodeur à trouver !!!!!!
int pwmA = 32; // (servo moteur succes) à mettre sur 7 lors du test carte
int pwmg = 16 ; //moteur gauche
int pwmg1 = 17 ; //moteur gauche
int pwmD = 19 ; //moteur droit
int pwmD1 = 18 ; //moteur droit
int canal1G = 0; // pwm canallg
int canal2G = 1; // pwm2G
int canal3D = 2; // pwm canal1D
int canal4D = 3; // pwm2D
int frequenceM = 1000 ; // pwm droit et gauche*/
int frequences = 50 ; 
int canal0 = 4 ; //servo
int frequence=50; // servo
int canal1=1; // servo
int frequence2 =500;// servo
int frequence3=1000;
int PWMPIN=32;
int CNYPIN=34;
int PWMCANAL0=0;

void setup()
 {
  Serial.begin(9600);
  pinMode(PWMPIN,OUTPUT);
  pinMode(CNYPIN, INPUT);

  pinMode(extd , INPUT);
  pinMode(intd, INPUT);
  pinMode(extg, INPUT);
  pinMode(intg , INPUT);

  ledcSetup(PWMCANAL0, frequence, resolution);
  ledcAttachPin(PWMPIN, PWMCANAL0);
  ledcSetup (canal0, frequences, resolution); //SERVO
  ledcSetup (canal2G, frequenceM, resolution); //PWMG
  ledcSetup (canal4D, frequenceM, resolution); // PWMD
  ledcAttachPin (pwmA, canal0); //servo
  ledcAttachPin (pwmg, canal1G); // Moteur gauche
  ledcAttachPin (pwmg1, canal2G); // Moteur gauche
  ledcAttachPin(pwmD, canal3D); // Moteur droit
  ledcAttachPin(pwmD1, canal4D); // Moteur droit
  // def servo mot
  ledcSetup(canal0, frequence, resolution);
  ledcSetup(canal1, frequence, resolution); 
  ledcAttachPin(pwmA, canal0); 

  // pour les capteurs 

  pinMode(PWMPIN,OUTPUT);
  pinMode(CNYPIN, INPUT);
  pinMode(extd , INPUT);
  pinMode(intd, INPUT);
  pinMode(extg, INPUT);
  pinMode(intg , INPUT);
  ledcSetup(PWMCANAL0, frequence3, resolution);
  ledcAttachPin(PWMPIN, PWMCANAL0);

  
}
int lecture_cap_din; // variable pour lire les capteurs CnY70 int lecture_cap_dex;
int lecture_cap_gex;
int lecture_cap_gin;
int lecture_cap_dex; 
void loop()
{
  extd=analogRead(extd);
  intd=analogRead(intd);
  extg=analogRead(extg);
  intg=analogRead(intg);

  while(1)
  {
  Serial.printf("extd  %d    intd  %d    extg  %d    intg  %d \n",extd,intd, extg, intg);
  lecture_cap_din = analogRead (intd);
  lecture_cap_dex = analogRead (intg);
  lecture_cap_gex = analogRead (extd);
  lecture_cap_gin = analogRead (extg);
  }
  ledcWrite(canal0, 102); //servo tourne à gauche
  // Serial.printf("servo ferme la pince \n");
  ledcWrite(canal0,40); //servo tourne à droite
  Serial.printf("servo ouvre la pince \n");
  // ledcWrite(canal1G,400);
  Serial.printf("moteur droit tourne \n");
  ledcWrite(canal3D,800);
  // Serial.printf("moteur gauche tourne \n");

// servo moteur
  ledcWrite(canal0, 60); 
  delay(20000); 
  ledcWrite(canal0, 100);
  delay(2000);


  // Serial.printf("cny1= %d \n cyn2=%d \n   cny3=%d \n    cny4=%d\n", lecture_cap_gex,lecture_cap_gin, lecture_cap_din, lecture_cap_dex);
}
