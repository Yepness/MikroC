// Nomes: Pablo Vinicius Oliveira 
//Declaração de Nomes dos Bits dos Ports
sbit V_CAFE at PORTA.B5;
sbit V_LEITE at PORTA.B6;
sbit V_CHOCO at PORTD.B0;
sbit B_CAFE at PORTC.B0;
sbit B_CAFE_LEITE at PORTC.B1;
sbit B_CHOCO at PORTC.B2;
sbit SENSOR_COPO at PORTA.B4;
sbit SERVO_PORTA at PORTE.B0;

// LCD module connections
sbit LCD_RS at PORTB.B4;
sbit LCD_EN at PORTB.B5;
sbit LCD_D4 at PORTB.B0;
sbit LCD_D5 at PORTB.B1;
sbit LCD_D6 at PORTB.B2;
sbit LCD_D7 at PORTB.B3;
sbit LCD_RS_Direction at TRISB4_bit;
sbit LCD_EN_Direction at TRISB5_bit;
sbit LCD_D4_Direction at TRISB0_bit;
sbit LCD_D5_Direction at TRISB1_bit;
sbit LCD_D6_Direction at TRISB2_bit;
sbit LCD_D7_Direction at TRISB3_bit;

void fecha() // -90 graus
{
 SERVO_PORTA=1;
 delay_us(1000);
 SERVO_PORTA=0;
 delay_us(20000);
}
void abre() // +90 graus
{
 SERVO_PORTA=1;
 delay_us(2000);
 SERVO_PORTA=0;
 delay_us(20000);
}
void cafe()
{
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,1," CAFE          ");
 abre();
 delay_ms(3000);
 LCD_Out(1,1," COLOQUE O COPO");
 LCD_Out(2,1,"               ");
 while(SENSOR_COPO ==0); // aguarda colocar o copo
 delay_ms(3000);
 fecha();
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,2," PREPARANDO    ");
 V_CAFE=1;
 delay_ms(10000);
 V_CAFE=0;
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,1," PRONTA        ");
 delay_ms(2000); // Delay incluido para melhor visualização
 abre();
 LCD_Out(1,1," RETIRAR COPO  ");
 LCD_Out(2,1,"               ");
 while(SENSOR_COPO ==1); // aguarda RETIRAR o copo
 delay_ms(3000);
 fecha();
}
void cafe_leite()
{
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,1," CAFE E LEITE  ");
 abre();
 delay_ms(3000);
 LCD_Out(1,1," COLOQUE O COPO");
 LCD_Out(2,1,"               ");
 while(SENSOR_COPO ==0); // aguarda colocar o copo
 delay_ms(3000);
 fecha();
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,2," PREPARANDO    ");
 V_LEITE=1;
 V_CAFE=1;
 delay_ms(10000);
 V_LEITE=0;
 V_CAFE=0;
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,1," PRONTA        ");
 delay_ms(2000); // Delay incluido para melhor visualização
 abre();
 LCD_Out(1,1," RETIRAR COPO  ");
 LCD_Out(2,1,"               ");
 while(SENSOR_COPO ==1); // aguarda RETIRAR o copo
 delay_ms(3000);
 fecha();
}
void chocolate()
{
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,1," CHOCOLATE     ");
 abre();
 delay_ms(3000);
 LCD_Out(1,1," COLOQUE O COPO");
 LCD_Out(2,1,"               ");
 while(SENSOR_COPO ==0); // aguarda colocar o copo
 delay_ms(3000);
 fecha();
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,2," PREPARANDO    ");
 V_CHOCO=1;
 V_LEITE=1;
 delay_ms(10000);
 V_CHOCO=0;
 V_LEITE=0;
 LCD_Out(1,1," BEBIDA:       ");
 LCD_Out(2,1," PRONTA        ");
 delay_ms(2000); // Delay incluido para melhor visualização
 abre();
 LCD_Out(1,1," RETIRAR COPO  ");
 LCD_Out(2,1,"               ");
 while(SENSOR_COPO ==1); // aguarda RETIRAR o copo
 delay_ms(3000);
 fecha();
}

// PROGRAMA PRINCIPAL

void main (void)
{
int temp, m;
float valorAD;
char comando, txt[7];
// Registradores de Configuração:
 ADCON1 = 0b00001110; // liga entrada AN0
 CMCON = 0b00000111;
// Configuração dos PORTS de Entrada e Saida
// 0 -> configura o BIT como Saída
// 1 -> configura o BIT como Entrada
// Exemplo: TRISA = 0b00001111;
 //76543210
 TRISA = 0b00010001; // A4 e A0 são entradas
 TRISC = 0b00000111; // C0 C1 C2 são entradas
 TRISD = 0b00000000;
 TRISE = 0b00000000;

 UART1_Init(9600);
 delay_ms(500);
 ADC_Init();
 LCD_Init();
 LCD_Cmd(_LCD_CURSOR_OFF);
 fecha();

//Inicio do Loop principal

while (1)
 {
 valorAD = adc_read(0);
 temp = (valorAD * 500)/1023; // converte para graus C

 while(temp <=80)
 {
 valorAD = adc_read(0);
 temp = (valorAD * 500)/1023; // converte para graus C


 LCD_Out(1,1," MAQUINA       ");
 LCD_Out(2,1," AQUECENDO     ");

 inttostr(temp,txt);
 ltrim(txt);
 LCD_OUT(2,12,txt);
 LCD_OUT_CP("C");
 m=1;
 }

 if(m==1)
 {
 LCD_Out(1,1," MAQUINA       ");
 LCD_Out(2,1," PRONTA        ");
 delay_ms(3000);
 m=0;
 }

 LCD_Out(1,1," Escolha       ");
 LCD_Out(2,1," Uma Opcao:    ");

 if( B_CAFE == 1 )
 {
 cafe();
 }
 if( B_CAFE_LEITE == 1 )
 {
 cafe_leite();
 }
 if( B_CHOCO == 1 )
 {
 chocolate();
 }

  if(UART1_Data_Ready())
 {
  comando = UART1_Read();

  if(comando == 'C') // CAFE
  {
  cafe();
  }

  if(comando == 'L') // CAFE COM LEITE
  {
  cafe_leite();
  }

  if(comando == 'H') // CHOCOLATE
  {
  chocolate();
  }
 }
 }//fecha o while
}//fecha o void main
