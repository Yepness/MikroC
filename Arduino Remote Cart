//Nome: Pablo Vinicius Oliveira 
//Simulador: Proteus 8 Ultimate
//Programa: MikroC For PIC

//Declaração de Nomes dos Bits dos Ports
//Exemplo:  sbit BOTAO at PORTA.b0;

sbit LCD_RS at RB4_bit;
sbit LCD_EN at RB5_bit;
sbit LCD_D7 at RB3_bit;
sbit LCD_D6 at RB2_bit;
sbit LCD_D5 at RB1_bit;
sbit LCD_D4 at RB0_bit;

sbit LCD_RS_Direction at TRISB4_bit;
sbit LCD_EN_Direction at TRISB5_bit;
sbit LCD_D7_Direction at TRISB3_bit;
sbit LCD_D6_Direction at TRISB2_bit;
sbit LCD_D5_Direction at TRISB1_bit;
sbit LCD_D4_Direction at TRISB0_bit;

sbit M1A at PORTC.B0;
sbit M1B at PORTC.B1;
sbit M2A at PORTC.B2;
sbit M2B at PORTC.B4;

sbit FAROL at PORTA.B1;
sbit LANTERNA at PORTA.B2;
sbit BUZINA at PORTA.B0;

void Frente()
{
 M1A = 1;
 M1B = 0;
 M2A = 1;
 M2B = 0;
}

void Tras()
{
 M1A = 0;
 M1B = 1;
 M2A = 0;
 M2B = 1;
}

void Parar()
{
 M1A = 0;
 M1B = 0;
 M2A = 1;
 M2B = 1;
}

void Esquerda()
{
 M1A = 0;
 M1B = 0;
 M2A = 1;
 M2B = 0;
}

void Direita()
{
 M1A = 1;
 M1B = 0;
 M2A = 0;
 M2B = 0;
}


//PROGRAMA PRINCIPAL

void main (void)
{  char comando;

// Registradores de Configuração:

        ADCON1 = 0b00001111;
        CMCON  = 0b00000111;

// Configuração dos PORTS de Entrada e Saida
// 0 -> configura o BIT como Saída
// 1 -> configura o BIT como Entrada
// Exemplo:  TRISA = 0b00001111;

        TRISC = 0b10000000;     // entrada serial
        TRISB = 0b00000000;
        TRISA = 0b00000000;



    UART1_Init(9600);
    delay_ms(500);

      Lcd_Init(); //inicia a função LCD
      LCD_Cmd(_LCD_CURSOR_OFF);

     M1A = 0;
     M1B = 0;
     M2A = 0;
     M2B = 0;

//Inicio do Loop principal

  while (1)
  {
     if(UART_Data_Ready())       //se receber um dado
      { comando = UART_read();  // leia o dado

        if(comando == 'F')      //Frente
         {  LCD_Out(1,1,"Carro: Frente   ");
            LCD_Out(2,2,"                ");
            Frente();
         }

         if(comando == 'B')   //Ré
         {  LCD_Out(1,1,"Carro: Tras     ");
            LCD_Out(2,2,"                ");
            Tras();
         }

         if(comando == 'L')      //Esquerda
         {  LCD_Out(1,1,"Carro: Esquerda ");
            LCD_Out(2,2,"                ");
            Esquerda();
         }

         if(comando == 'R')   //Direita
         {  LCD_Out(1,1,"Carro: Direita  ");
            LCD_Out(2,2,"                ");
           Direita();
         }

         if(comando == 'S')   //Parado
         {  LCD_Out(1,1,"Carro: Parado   ");
            LCD_Out(2,2,"                ");
            Parar();
         }


         if(comando == 'W')
         {  LCD_Out(1,1,"Carro: Parado   "); //Farol
            LCD_Out(2,2,"      Farol     ");
            FAROL = 1;
            Parar();
         }

         if(comando == 'w')
         {  LCD_Out(1,1,"Carro: Parado   ");
            LCD_Out(2,2,"                ");
            FAROL = 0;
            Parar();
         }
         

         if(comando == 'U')
         {  LCD_Out(1,1,"Carro: Frente   ");   //Lanterna
            LCD_Out(2,2,"      Lanterna  ");
            LANTERNA = 1;
            Frente();
         }

         if(comando == 'u')
         {  LCD_Out(1,1,"Carro: Frente   ");
            LCD_Out(2,2,"                ");
            LANTERNA = 0;
            Frente();
         }


         if(comando == 'V')
         {  LCD_Out(1,1,"Carro: Frente   "); //Buzina
            LCD_Out(2,2,"     Buzina     ");
            BUZINA = 1;
            Frente();
         }

         if(comando == 'v')
         {  LCD_Out(1,1,"Carro: Frente   ");
            LCD_Out(2,2,"                ");
            BUZINA = 0;
            Frente();
         }
      
          else
         if(((BUZINA =='0') && (LANTERNA == '1') && (FAROL =='1')))
         {  LCD_Out(1,1,"Carro: Frente   ");    //Farol e lanterna
            LCD_Out(2,2,"  Farol e Lant  ");
            Frente();
         }


         if(((BUZINA =='1') && (LANTERNA == '1') && (FAROL =='1')))
         {  LCD_Out(1,1,"Carro: Frente   ");    //Buzina, Farol e lanterna
            LCD_Out(2,2,"Lant BZ e Farol ");
            Frente();
         }

         if(((BUZINA =='0') && (LANTERNA == '1') && (FAROL =='1')))
         {  LCD_Out(1,1,"Carro: Frente   ");    //Farol e lanterna
            LCD_Out(2,2,"  Farol e Lant  ");
            Frente();
         }
         
         if(((BUZINA =='0') && (LANTERNA == '0') && (FAROL =='1')))
         {  LCD_Out(1,1,"Carro: Parado   ");    //Farol e lanterna
            LCD_Out(2,2,"  Farol         ");
            Parar();
         }
         
         if(((BUZINA =='0') && (LANTERNA == '1') && (FAROL =='0')))
         {  LCD_Out(1,1,"Carro: Frente   ");    //Farol e lanterna
            LCD_Out(2,2," Lanterna       ");
            Frente();
         }
      }


  }//fecha o while
}//fecha o void main
