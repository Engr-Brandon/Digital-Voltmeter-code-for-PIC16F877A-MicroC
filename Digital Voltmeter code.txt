//
sbit LCD_RS at RB0_bit;
sbit LCD_EN at RB1_bit;
sbit LCD_D4 at RB2_bit;
sbit LCD_D5 at RB3_bit;
sbit LCD_D6 at RB4_bit;
sbit LCD_D7 at RB5_bit;
//directions
sbit LCD_RS_Direction at TRISB0_bit;
sbit LCD_EN_Direction at TRISB1_bit;
sbit LCD_D4_Direction at TRISB2_bit;
sbit LCD_D5_Direction at TRISB3_bit;
sbit LCD_D6_Direction at TRISB4_bit;
sbit LCD_D7_Direction at TRISB5_bit;
//
float voltage, Displayvolt;
char volt[4];
void main(){
  TRISB=0X00;    //all portB as outputs
  TRISA=0X0F;    //0000 1111   PORTA0 as input
  //
  Lcd_Init();    //initialize the LCD
  ADC_Init();     //initialize the ADC
  //
  Lcd_Cmd(_LCD_CLEAR);     //clear the LCD
  Lcd_Cmd(_LCD_CURSOR_OFF);   //set the cursor off
  Lcd_Out(1,5,"Digital");
  Lcd_Out(2,4,"Voltmeter");//display the messages on the LCD
  delay_ms(2000);
  //
  Lcd_Cmd(_LCD_CLEAR);     //clear the LCD
  Lcd_Cmd(_LCD_CURSOR_OFF);   //set the cursor off
  Lcd_Out(1,3,"Designed by");
  Lcd_Out(2,3,"Engr Brandon");//display the messages on the LCD
  delay_ms(3000);
  //
  Lcd_Cmd(_LCD_CLEAR);
  Lcd_Cmd(_LCD_CURSOR_OFF);
  //
  while(1){
    voltage=ADC_Read(RA0);    //read the input voltage
    floattostr(Displayvolt,volt);
    //
    Lcd_Out(1,3,"Voltage=");
    Displayvolt=(voltage*5)/1023;
    Lcd_Out(2,12,Rtrim(volt));
    Lcd_Out(2,16,"V");
    Lcd_Cmd(_LCD_CURSOR_OFF);
    delay_ms(300);
  }
}