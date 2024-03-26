﻿# Projet-VSCode
 
#include <Arduino.h>

int pwmA = 32;

int frequence = 50;
int canal0 = 0;
int canal1 = 1;
int resolution = 10;

void setup()
{
  ledcSetup(canal0, frequence, resolution);
  ledcSetup(canal1, frequence, resolution);

  ledcAttachPin(pwmA, canal0);
}

void loop()
{
  ledcWrite(canal0, 45);
  delay(2000);
  ledcWrite(canal0, 60);
  delay(2000);
}
