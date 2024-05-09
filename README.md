### NAME:Kowsalya M
### REG.NO:212222230069
# EX:06 SQUARE WAVE GENERATION AT THE OUTPUT PIN USING TIMER

### Aim:
To generate a PWM wave at the timer pin output and  simuate it on  proteus using an virtual oscilloscope  

### Components required:
STM32 CUBE IDE, Proteus 8 simulator .

### Theory:

The timer modules can operate a variety of modes one of which is the PWM mode. Where the timer gets clocked from an internal source and counts up to the auto-reload register value, then the output channel pin is driven HIGH. And it remains until the timer counts reach the CCRx register value, the match event causes the output channel pin to be driven LOW. And it remains until the timer counts up to the auto-reload register value, and so on.

The resulting waveform is called PWM (pulse-width modulated) signal. Whose frequency is determined by the internal clock, the Prescaler, and the ARRx register. And its duty cycle is defined by the channel CCRx register value. The PWM doesn’t always have to be following this exact same procedure for PWM generation, however, it’s the very basic one and the easier to understand the concept. It’s called the up-counting PWM mode. We’ll discuss further advanced PWM generation techniques as we go on in this series of tutorials.

The following diagram shows you how the ARR value affects the period (frequency) of the PWM signal. And how the CCRx value affects the corresponding PWM signal’s duty cycle. And illustrates the whole process of PWM signal generation in the up-counting normal mode.

STM32 Timers – PWM Output Channels

Each Capture/Compare channel is built around a capture/compare register (including a shadow register), an input stage for capture (with a digital filter, multiplexing, and Prescaler) and an output stage (with comparator and output control). The output stage generates an intermediate waveform which is then used for reference: OCxRef (active high). The polarity acts at the end of the chain.
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/87457b57-4311-440b-8cbe-a9d78db4335a)

STM32 Timers In PWM Mode

Pulse width modulation mode allows generating a signal with a frequency determined by the value of the TIMx_ARR register and a duty cycle determined by the value of the TIMx_CCRx register. The PWM mode can be selected independently on each channel (one PWM per OCx output) by writing 110 (PWM mode 1) or ‘111 (PWM mode 2) in the OCxM bits in the TIMx_CCMRx register. The user must enable the corresponding preload register by setting the OCxPE bit in the TIMx_CCMRx register, and eventually the auto-reload preload register by setting the ARPE bit in the TIMx_CR1 register.

OCx polarity is software programmable using the CCxP bit in the TIMx_CCER register. It can be programmed as active high or active low. For applications where you need to generate complementary PWM signals, this option will be suitable for you.

In PWM mode (1 or 2), TIMx_CNT and TIMx_CCRx are always compared to determine whether TIMx_CCRx≤TIMx_CNT or TIMx_CNT≤TIMx_CCRx (depending on the direction of the counter).

The timer is able to generate PWM in edge-aligned mode or center-aligned mode depending on the CMS bits in the TIMx_CR1 register.
STM32 PWM Frequency

In various applications, you’ll be in need to generate a PWM signal with a specific frequency. In servo motor control, LED drivers, motor drivers, and many more situations where you’ll be in need to set your desired frequency for the output PWM signal.

The PWM period (1/FPWM) is defined by the following parameters: ARR value, the Prescaler value, and the internal clock itself which drives the timer module FCLK. The formula down below is to be used for calculating the FPWM for the output. You can set the clock you’re using, the Prescaler, and solve for the ARR value in order to control the FPWM and get what you want.

STM32 PWM Frequency Formula - STM32 PWM Frequency Equation
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/aca8a20e-9b99-40c1-bada-f31accaa2ae9)

STM32 PWM Duty Cycle

In normal settings, assuming you’re using the timer module in PWM mode and generating PWM signal in edge-aligned mode up-counting configuration. The duty cycle percentage is controlled by changing the value of the CCRx register. And the duty cycle equals (CCRx/ARR) [%].
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/58ce0807-331e-49f7-bc8d-373f82592a92)



## Procedure:
Step1: Open CubeMX & Create New Project

Step2: Choose The Target MCU & Double-Click Its Name select the target to be programmed  as shown below and click on next 

Step3: Configure Timer2 Peripheral To Operate In PWM Mode With CH1 Output

Step4: Set The RCC External Clock Source

STM32 RCC External Clock Selection CubeMX

Step5: Go To The Clock Configuration

Step6: Set The System Clock To Be 72MHz

Step7: Name & Generate The Project Initialization Code For CubeIDE or The IDE You’re Using

Step8:  Creating Proteus project and running the simulation
We are now at the last part of step by step guide on how to simulate STM32 project in Proteus.

Step9: Create a new Proteus project and place STM32F40xx i.e. the same MCU for which the project was created in STM32Cube IDE. 
After creation of the circuit as per requirement as shown below 

Step10. Double click on the the MCU part to open settings. Next to the Program File option, give full path to the Hex file generated using STM32Cube IDE. Then set the external crystal frequency to 8M (i.e. 8 MHz). Click OK to save the changes.

Step11: click on debug and simulate using simulation as shown below 


## STM 32 CUBE PROGRAM :
```
HAL_TIM_Base_Start(&htim2);
HAL_TIM_PWM_Init(&htim2);
HAL_TIM_PWM_Start(&htim2,TIM_CHANNEL_1);
```

## Output screen shots of proteus  :
 ![6-1](https://github.com/Divya110205/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/119404855/32210120-96c0-4973-82bf-e2e672a4c889)

 
## CIRCUIT DIAGRAM (EXPORT THE GRAPHICS TO PDF AND ADD THE SCREEN SHOT HERE): 
 ![6-2](https://github.com/Divya110205/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/119404855/ca50af39-d3f7-4580-b098-8ad0b46e2f8f)


## DUTY CYCLE AND FREQUENCY CALCULATION 
FOR PULSE AT 500
![6-3](https://github.com/Divya110205/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/119404855/5a9c4db9-6a1c-4a4d-b7f5-1c797cc2aaf0)

TON = 0.34 ms

TOFF= 0.34 ms

TOTAL TIME = TON +TOFF = 0.64 ms

FREQUENCY = 1/(TOTAL TIME) = 1/0.64 = 1562.5 Hertz.
FOR PULSE AT 700
![6-4](https://github.com/Divya110205/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/119404855/8e7a905d-34c1-408a-8222-6577b4e19d91)

TON = 0.85 ms

TOFF= 0.34 ms

TOTAL TIME = TON +TOFF = 0.85+0.34 = 1.18 ms

FREQUENCY = 1/(TOTAL TIME) = 1/1.18 = 847.45 Hertz


FOR PULSE AT 900
![6-5](https://github.com/Divya110205/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/119404855/e8776909-f995-4830-9c26-b044fdce5545)

TON = 1.08 ms

TOFF=0.12 ms

TOTAL TIME = TON + TOFF = 1.08+0.12 = 1.2 ms

FREQUENCY = 1/(TOTAL TIME) = 1/1.2 = 833.33 Hertz


## Result :
A PWM Signal is generated using the following frequency and various duty cycles are simulated 




