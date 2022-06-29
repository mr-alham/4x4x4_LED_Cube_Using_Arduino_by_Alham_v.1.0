```c++
#include<Arduino.h>

int column[16] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, A0, A1}; //initializing and declaring led rows
int layer[4] = {A2, A3, A4, A5}; //initializing and declaring led layersint pot_value = 0;  //defined a variouble to store potentiometers valueint lamp_state = 0;  //defined this variouble to store the last step of lamp's LED state (so the loop dosen't have to go once again to switch case )int mapped_pot_value = 0;  //maped value of pot valueint switch_current_state = 0;  //defined a variouble to store switch's state

void setup() {  //this will run only once at startup
  for (int i = 0; i < 16; i++) { //setting columns to OUTPUT
    pinMode(column[i], OUTPUT);

  }
  for (int i = 0; i < 4; i++) { //setting layers to OUTPUT
    pinMode(layer[i], OUTPUT);

  }
  randomSeed(analogRead(10));  //randomly seeding for RANDOM PATTERN

  for (int i = 0; i != 350; i += 2) { //before start cube will light for random pattern
    int random_layer = random(0, 4);
    int random_column = random(0, 16);

    digitalWrite(column[random_column], HIGH);
    digitalWrite(layer[random_layer], HIGH);
    delay(6);
    digitalWrite(column[random_column], LOW);
    digitalWrite(layer[random_layer], LOW);
    delay(6);

  }
  off_the_cube();  //turn off whole cube

}
void loop() {  //things in loop function will run again and again and again repeatedly


  around_edge_down();  //1
  layers_to_up_and_down();  //2
  shaking();  //3
  on_the_whole_cube();  //4
  delay(700);
  on_and_off_layers_up_down_not_timed();  //5
  on_the_whole_cube();  //6
  columns_on_off_side_ways();  //7
  random_flicker();  //8
  random_rain();  //9
  go_through_all_leds_one_at_time();  //10
  propeller();  //11
  spiral_in_and_out();  //12
  diagonal_rectangle();  //13
  random_pattern();  //14
  delay(1500);


}
void off_the_cube() {  //this function will turn off whole cube
  for (int i = 0; i < 16; i++) {
    digitalWrite(column[i], HIGH);

  }
  for (int i = 0; i < 4; i++) {
    digitalWrite(layer[i], LOW);

  }
}
void on_the_whole_cube() {  //this function will TURN ON WHOLE LIGHTS of the cube
  for (int i = 0; i < 16; i++) {
    digitalWrite(column[i], LOW);

  }
  for (int i = 0; i < 4; i++) {
    digitalWrite(layer[i], HIGH);

  }
}
void turn_columns_off() {  //this function will turn off all columns only
  for (int i = 0; i < 16; i++) {
    digitalWrite(column[i], 1);

  }
}
void shaking() {  //in this function cube's ON OFF SPEED will increase gradually like SHAKING
  for (int shake_delay = 170; shake_delay > 15; shake_delay -= 3) {
    for (int i = 0; i < 16; i++) {
      digitalWrite(column[i], LOW);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(layer[i], HIGH);

    }
    delay(shake_delay);
    for (int i = 0; i < 16; i++) {
      digitalWrite(column[i], HIGH);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(layer[i], LOW);

    }
    delay(shake_delay);

    if (shake_delay < 40) {
      for (int i = 0; i < 16; i++) {
        digitalWrite(column[i], LOW);

      }
      for (int i = 0; i < 4; i++) {
        digitalWrite(layer[i], HIGH);

      }
      delay(shake_delay);

      for (int i = 0; i < 16; i++) {
        digitalWrite(column[i], HIGH);

      }
      for (int i = 0; i < 4; i++) {
        digitalWrite(layer[i], LOW);

      }
      delay(shake_delay);

    }
  }
}
void shaking_opposite() {   //this fundtion will do the OPPOSITE of above shaking function and cube's ON OFF SPEED WILL gradually decrease
  for (int shake_delay = 0; shake_delay < 110; shake_delay += 4) {
    for (int i = 0; i < 16; i++) {
      digitalWrite(column[i], LOW);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(layer[i], HIGH);

    }
    delay(shake_delay);
    for (int i = 0; i < 16; i++) {
      digitalWrite(column[i], HIGH);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(layer[i], LOW);

    }
    delay(shake_delay);

  }
}
void on_and_off_layers_up_down_not_timed() {
  int delay_time = 150;
  for (int i = 2; i != 0; i--) {
    on_the_whole_cube();
    for (int i = 4; i != 0; i--) {
      digitalWrite(layer[i - 1], 0);
      delay(delay_time);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(layer[i], 1);
      delay(delay_time);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(layer[i], 0);
      delay(delay_time);

    }
    for (int i = 4; i != 0; i--) {
      digitalWrite(layer[i - 1], 1);
      delay(delay_time);

    }
  }
}
void layers_to_up_and_down() {  //this function will turn on and off layers to a art
  on_the_whole_cube();
  int x = 50;
  for (int i = 0; i < 4; i++) {
    digitalWrite(layer[i], 0);

  }
  for (int y = 0; y < 7; y++) {
    for (int count = 0; count < 1; count++) {
      if (x >= 100) {
        x = 100;

      }
      else {
        x += 15;

      }
      for (int i = 0; i < 4; i++) {
        digitalWrite(layer[i], 1);
        delay(x);
        digitalWrite(layer[i], 0);

      }
      for (int i = 4; i != 0; i--) {
        digitalWrite(layer[i - 1], 1);
        delay(x);
        digitalWrite(layer[i - 1], 0);

      }
    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(layer[i], 1);
      delay(x);

    }
    for (int i = 4; i != 0; i--) {
      delay(x);
      digitalWrite(layer[i - 1], 0);
      delay(x);

    }
  }
  delay(190);

}
void columns_on_off_side_ways() {
  int x = 75;
  off_the_cube();
  for (int i = 0; i < 4; i++) {
    digitalWrite(layer[i], 1);

  }
  for (int y = 0; y < 3; y++) {
    for (int i = 0; i < 4; i++) {
      digitalWrite(column[i], 0);
      delay(x);

    }
    for (int i = 4; i < 8; i++) {
      digitalWrite(column[i], 0);
      delay(x);

    }
    for (int i = 8; i < 12; i++) {
      digitalWrite(column[i], 0);
      delay(x);

    }
    for (int i = 12; i < 16; i++) {
      digitalWrite(column[i], 0);
      delay(x);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(column[i], 1);
      delay(x);

    }
    for (int i = 4; i < 8; i++) {
      digitalWrite(column[i], 1);
      delay(x);

    }
    for (int i = 8; i < 12; i++) {
      digitalWrite(column[i], 1);
      delay(x);

    }
    for (int i = 12; i < 16; i++) {
      digitalWrite(column[i], 1);
      delay(x);

    }
    for (int i = 12; i < 16; i++) {
      digitalWrite(column[i], 0);
      delay(x);

    }
    for (int i = 8; i < 12; i++) {
      digitalWrite(column[i], 0);
      delay(x);

    }
    for (int i = 4; i < 8; i++) {
      digitalWrite(column[i], 0);
      delay(x);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(column[i], 0);
      delay(x);

    }
    for (int i = 12; i < 16; i++) {
      digitalWrite(column[i], 1);
      delay(x);

    }
    for (int i = 8; i < 12; i++) {
      digitalWrite(column[i], 1);
      delay(x);

    }
    for (int i = 4; i < 8; i++) {
      digitalWrite(column[i], 1);
      delay(x);

    }
    for (int i = 0; i < 4; i++) {
      digitalWrite(column[i], 1);
      delay(x);

    }
  }
}
void around_edge_down() {
  int delay_y = 150;
  for (int i = 1; i < 5; i++) {
    delay_y -= 17;
    digitalWrite(layer[i - 1], 1);
    digitalWrite(column[5], 0);
    digitalWrite(column[6], 0);
    digitalWrite(column[9], 0);
    digitalWrite(column[10], 0);

    digitalWrite(column[0], 0);
    delay(delay_y);

    digitalWrite(column[0], 1);
    digitalWrite(column[4], 0);
    delay(delay_y);

    digitalWrite(column[4], 1);
    digitalWrite(column[8], 0);
    delay(delay_y);

    digitalWrite(column[8], 1);
    digitalWrite(column[12], 0);
    delay(delay_y);

    digitalWrite(column[12], 1);
    digitalWrite(column[13], 0);
    delay(delay_y);

    digitalWrite(column[13], 1);
    digitalWrite(column[15], 0);
    delay(delay_y);

    digitalWrite(column[15], 1);
    digitalWrite(column[14], 0);
    delay(delay_y);

    digitalWrite(column[14], 1);
    digitalWrite(column[11], 0);
    delay(delay_y);

    digitalWrite(column[11], 1);
    digitalWrite(column[7], 0);
    delay(delay_y);

    digitalWrite(column[7], 1);
    digitalWrite(column[3], 0);
    delay(delay_y);

    digitalWrite(column[3], 1);
    digitalWrite(column[2], 0);
    delay(delay_y);

    digitalWrite(column[2], 1);
    digitalWrite(column[1], 0);
    delay(delay_y);

    digitalWrite(column[1], 1);

  }
  for (int x = 200; x != 0; x -= 50) {
    off_the_cube();
    for (int i = 4; i != 0; i--) {
      digitalWrite(layer[i - 1], 1);
      digitalWrite(column[5], 0);
      digitalWrite(column[6], 0);
      digitalWrite(column[9], 0);
      digitalWrite(column[10], 0);
      digitalWrite(column[0], 0);
      delay(x);

      digitalWrite(column[0], 1);
      digitalWrite(column[4], 0);
      delay(x);

      digitalWrite(column[4], 1);
      digitalWrite(column[8], 0);
      delay(x);

      digitalWrite(column[8], 1);
      digitalWrite(column[12], 0);
      delay(x);

      digitalWrite(column[12], 1);
      digitalWrite(column[13], 0);
      delay(x);

      digitalWrite(column[13], 1);
      digitalWrite(column[15], 0);
      delay(x);

      digitalWrite(column[15], 1);
      digitalWrite(column[14], 0);
      delay(x);

      digitalWrite(column[14], 1);
      digitalWrite(column[11], 0);
      delay(x);

      digitalWrite(column[11], 1);
      digitalWrite(column[7], 0);
      delay(x);

      digitalWrite(column[7], 1);
      digitalWrite(column[3], 0);
      delay(x);

      digitalWrite(column[3], 1);
      digitalWrite(column[2], 0);
      delay(x);

      digitalWrite(column[2], 1);
      digitalWrite(column[1], 0);
      delay(x);

      digitalWrite(column[1], 1);

    }
  }
}
void random_flicker() {  //this function will on LED'S on random pattern
  off_the_cube();
  int x = 100;
  for (int i = 0; i != 300; i += 2) {
    int randomLayer = random(0, 4);
    int randomColumn = random(0, 16);

    digitalWrite(layer[randomLayer], 1);
    digitalWrite(column[randomColumn], 0);
    delay(x);

    digitalWrite(layer[randomLayer], 0);
    digitalWrite(column[randomColumn], 1);
    delay(x);

  }
}
void random_rain() {  //this function will show as LED's as raining
  off_the_cube();
  int x = 150;
  for (int i = 0; i != 60; i += 2) {
    int randomColumn = random(0, 16);
    digitalWrite(column[randomColumn], 0);
    digitalWrite(layer[3], 1);
    delay(x + 70);

    digitalWrite(layer[2], 1);
    delay(x);
    digitalWrite(layer[3], 0);
    delay(x);
    digitalWrite(layer[1], 1);
    delay(x);
    digitalWrite(layer[2], 0);
    delay(x);
    digitalWrite(layer[0], 1);
    delay(x);
    digitalWrite(layer[1], 0);
    delay(x);
    digitalWrite(layer[0], 0);
    digitalWrite(column[randomColumn], 1);

  }
}
void diagonal_rectangle() {
  int x = 350;
  off_the_cube();
  for (int count = 0; count < 5; count++) {
    for (int i = 0; i < 8; i++) {
      digitalWrite(column[i], 0);

    }
    digitalWrite(layer[3], 1);
    digitalWrite(layer[2], 1);
    delay(x);
    off_the_cube();
    for (int i = 4; i < 12; i++) {
      digitalWrite(column[i], 0);

    }
    digitalWrite(layer[1], 1);
    digitalWrite(layer[2], 1);
    delay(x);
    off_the_cube();
    for (int i = 8; i < 16; i++) {
      digitalWrite(column[i], 0);

    }
    digitalWrite(layer[0], 1);
    digitalWrite(layer[1], 1);
    delay(x);
    off_the_cube();
    for (int i = 4; i < 12; i++) {
      digitalWrite(column[i], 0);

    }
    digitalWrite(layer[0], 1);
    digitalWrite(layer[1], 1);
    delay(x);
    off_the_cube();
    for (int i = 0; i < 8; i++) {
      digitalWrite(column[i], 0);

    }
    digitalWrite(layer[0], 1);
    digitalWrite(layer[1], 1);
    delay(x);
    off_the_cube();
    for (int i = 4; i < 12; i++) {
      digitalWrite(column[i], 0);

    }
    digitalWrite(layer[1], 1);
    digitalWrite(layer[2], 1);
    delay(x);
    off_the_cube();
    for (int i = 8; i < 16; i++) {
      digitalWrite(column[i], 0);

    }
    digitalWrite(layer[2], 1);
    digitalWrite(layer[3], 1);
    delay(x);
    off_the_cube();
    for (int i = 4; i < 12; i++) {
      digitalWrite(column[i], 0);

    }
    digitalWrite(layer[2], 1);
    digitalWrite(layer[3], 1);
    delay(x);
    off_the_cube();

  }
  for (int i = 0; i < 8; i++) {
    digitalWrite(column[i], 0);

  }
  digitalWrite(layer[3], 1);
  digitalWrite(layer[2], 1);
  delay(x);
  off_the_cube();

}
void go_through_all_leds_one_at_time() {
  int x = 15;
  off_the_cube();
  for (int y = 0; y < 5; y++) {
    for (int count = 4; count != 0; count--) {
      digitalWrite(layer[count - 1], 1);
      for (int i = 0; i < 4; i++) {
        digitalWrite(column[i], 0);
        delay(x);
        digitalWrite(column[i], 1);
        delay(x);

      }
      digitalWrite(layer[count - 1], 0);

    }
    for (int count = 0; count < 4; count++) {
      digitalWrite(layer[count], 1);
      for (int i = 4; i < 8; i++) {
        digitalWrite(column[i], 0);
        delay(x);
        digitalWrite(column[i], 1);
        delay(x);

      }
      digitalWrite(layer[count], 0);

    }
    for (int count = 4; count != 0; count--) {
      digitalWrite(layer[count - 1], 1);
      for (int i = 8; i < 12; i++) {
        digitalWrite(column[i], 0);
        delay(x);
        digitalWrite(column[i], 1);
        delay(x);

      }
      digitalWrite(layer[count - 1], 0);

    }
    for (int count = 0; count < 4; count++) {
      digitalWrite(layer[count], 1);
      for (int i = 12; i < 16; i++) {
        digitalWrite(column[i], 0);
        delay(x);
        digitalWrite(column[i], 1);
        delay(x);

      }
      digitalWrite(layer[count], 0);

    }
  }
}
void propeller() {
  off_the_cube();
  int x = 90;
  for (int y = 4; y > 0; y--) {
    for (int i = 0; i < 6; i++) {
      digitalWrite(layer[y - 1], 1);
      turn_columns_off();
      digitalWrite(column[0], 0);
      digitalWrite(column[5], 0);
      digitalWrite(column[10], 0);
      digitalWrite(column[15], 0);
      delay(x);

      turn_columns_off();
      digitalWrite(column[4], 0);
      digitalWrite(column[5], 0);
      digitalWrite(column[10], 0);
      digitalWrite(column[11], 0);
      delay(x);

      turn_columns_off();
      digitalWrite(column[6], 0);
      digitalWrite(column[7], 0);
      digitalWrite(column[8], 0);
      digitalWrite(column[9], 0);
      delay(x);

      turn_columns_off();
      digitalWrite(column[3], 0);
      digitalWrite(column[6], 0);
      digitalWrite(column[9], 0);
      digitalWrite(column[12], 0);
      delay(x);

      turn_columns_off();
      digitalWrite(column[2], 0);
      digitalWrite(column[6], 0);
      digitalWrite(column[9], 0);
      digitalWrite(column[13], 0);
      delay(x);

      turn_columns_off();
      digitalWrite(column[1], 0);
      digitalWrite(column[5], 0);
      digitalWrite(column[10], 0);
      digitalWrite(column[14], 0);
      delay(x);

    }
  }
  turn_columns_off();
  digitalWrite(column[0], 0);
  digitalWrite(column[5], 0);
  digitalWrite(column[10], 0);
  digitalWrite(column[15], 0);
  delay(x);

}
void spiral_in_and_out() {
  on_the_whole_cube();
  int x = 60;
  for (int i = 0; i < 6; i++) {
    digitalWrite(column[0], 1);
    delay(x);
    digitalWrite(column[1], 1);
    delay(x);
    digitalWrite(column[2], 1);
    delay(x);
    digitalWrite(column[3], 1);
    delay(x);
    digitalWrite(column[7], 1);
    delay(x);
    digitalWrite(column[11], 1);
    delay(x);
    digitalWrite(column[15], 1);
    delay(x);
    digitalWrite(column[14], 1);
    delay(x);
    digitalWrite(column[13], 1);
    delay(x);
    digitalWrite(column[12], 1);
    delay(x);
    digitalWrite(column[8], 1);
    delay(x);
    digitalWrite(column[4], 1);
    delay(x);
    digitalWrite(column[5], 1);
    delay(x);
    digitalWrite(column[6], 1);
    delay(x);
    digitalWrite(column[10], 1);
    delay(x);
    digitalWrite(column[9], 1);
    delay(x);

    digitalWrite(column[9], 0);
    delay(x);
    digitalWrite(column[10], 0);
    delay(x);
    digitalWrite(column[6], 0);
    delay(x);
    digitalWrite(column[5], 0);
    delay(x);
    digitalWrite(column[4], 0);
    delay(x);
    digitalWrite(column[8], 0);
    delay(x);
    digitalWrite(column[12], 0);
    delay(x);
    digitalWrite(column[13], 0);
    delay(x);
    digitalWrite(column[14], 0);
    delay(x);
    digitalWrite(column[15], 0);
    delay(x);
    digitalWrite(column[11], 0);
    delay(x);
    digitalWrite(column[7], 0);
    delay(x);
    digitalWrite(column[3], 0);
    delay(x);
    digitalWrite(column[2], 0);
    delay(x);
    digitalWrite(column[1], 0);
    delay(x);
    digitalWrite(column[0], 0);
    delay(x);

    digitalWrite(column[0], 1);
    delay(x);
    digitalWrite(column[4], 1);
    delay(x);
    digitalWrite(column[8], 1);
    delay(x);
    digitalWrite(column[12], 1);
    delay(x);
    digitalWrite(column[13], 1);
    delay(x);
    digitalWrite(column[14], 1);
    delay(x);
    digitalWrite(column[15], 1);
    delay(x);
    digitalWrite(column[11], 1);
    delay(x);
    digitalWrite(column[7], 1);
    delay(x);
    digitalWrite(column[3], 1);
    delay(x);
    digitalWrite(column[2], 1);
    delay(x);
    digitalWrite(column[1], 1);
    delay(x);
    digitalWrite(column[5], 1);
    delay(x);
    digitalWrite(column[9], 1);
    delay(x);
    digitalWrite(column[10], 1);
    delay(x);
    digitalWrite(column[6], 1);
    delay(x);

    digitalWrite(column[6], 0);
    delay(x);
    digitalWrite(column[10], 0);
    delay(x);
    digitalWrite(column[9], 0);
    delay(x);
    digitalWrite(column[5], 0);
    delay(x);
    digitalWrite(column[1], 0);
    delay(x);
    digitalWrite(column[2], 0);
    delay(x);
    digitalWrite(column[3], 0);
    delay(x);
    digitalWrite(column[7], 0);
    delay(x);
    digitalWrite(column[11], 0);
    delay(x);
    digitalWrite(column[15], 0);
    delay(x);
    digitalWrite(column[14], 0);
    delay(x);
    digitalWrite(column[13], 0);
    delay(x);
    digitalWrite(column[12], 0);
    delay(x);
    digitalWrite(column[8], 0);
    delay(x);
    digitalWrite(column[4], 0);
    delay(x);
    digitalWrite(column[0], 0);
    delay(x);
  }
}
void on_all_column() {  //this function will turn on all columns
  for (int i = 0; i < 16; i++) {
    digitalWrite(column[i], LOW);

  }
}
void on_all_layers() {  //this function will turn on all layers
  for (int i = 0; i < 4; i++) {
    digitalWrite(layer[i], HIGH);

  }
}
void random_pattern() {  //this function will on and off led's randomly
  for (int i = 0; i != 350; i += 2) {
    int random_layer = random(0, 4);
    int random_column = random(0, 16);

    digitalWrite(column[random_column], HIGH);
    digitalWrite(layer[random_layer], HIGH);
    delay(6);
    digitalWrite(column[random_column], LOW);
    digitalWrite(layer[random_layer], LOW);
    delay(6);

  }
}
```
//END of the code.

