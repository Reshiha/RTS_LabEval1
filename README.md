PART 1 - STM32 - implement ring buffer to recive from UART 

STEPS NEED TO BE FOLLOWED:-
1. Put the following statements in the interrupt.c file
     extern void Uart_isr (UART_HandleTypeDef *huart);
     extern uint16_t timeout;
2. Change the systick handler in the interrupt.c file again
   void SysTick_Handler(void)
{
  /* USER CODE BEGIN SysTick_IRQn 0 */
  
  if(timeout >0)  timeout--;

  /* USER CODE END SysTick_IRQn 0 */
  HAL_IncTick();
  /* USER CODE BEGIN SysTick_IRQn 1 */

  /* USER CODE END SysTick_IRQn 1 */
}
3. Modify the Uart_IRQ_Handler according to uart that you are using.. like shown below
void USART2_IRQHandler(void)
{
  /* USER CODE BEGIN USART2_IRQn 0 */

  Uart_isr (&huart2);

  /* USER CODE END USART2_IRQn 0 */
//  HAL_UART_IRQHandler(&huart2);
  /* USER CODE BEGIN USART2_IRQn 1 */

  /* USER CODE END USART2_IRQn 1 */
}
4. put the Ringbuf_init (); in the main function and you are good to go




PART 2 - UART RING BUFFER through DMA

1. In the STM32CubeMX, enable the UART interrupt
2. In the DMA section, use the NORMAL mode.
3. IN the Generated code, make sure the DMA is initialized before the UART. CubeMX sometimes does the opposite and in that case, DMA won't work.
4. Change the UART and the DMA in the uartRingBuffDMA.c file
5. Define the RxBuf and MainBuf Sizes
6. check how the timeout is defined as the external variable in the STM32xxxxIT.c file. Also put the TIMEOUT-- in the systick handler
7. check the main file to see the usage of the functions



