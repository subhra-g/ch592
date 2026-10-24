cmake_minimum_required(VERSION 3.23)

set(lib ch59x.hal.peripheral)

add_library(${lib} STATIC)

# HAL Peripherals
target_sources(${lib}
	PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/ISP592.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_adc.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_clk.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_common.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_flash.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_gpio.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_i2c.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_lcd.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_pwm.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_pwr.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_spi.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_sys.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_timer.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_uart.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_usbdev.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH59x_usbhost.h>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/CH592SFR.h>
	#
	$<INSTALL_INTERFACE:include/ch59x/peripheral/ISP592.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_adc.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_clk.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_common.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_flash.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_gpio.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_i2c.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_lcd.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_pwm.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_pwr.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_spi.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_sys.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_timer.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_uart.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_usbdev.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH59x_usbhost.h>
	$<INSTALL_INTERFACE:include/ch59x/peripheral/CH592SFR.h>
	PRIVATE
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_pwm.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_pwr.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_spi0.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_sys.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_timer0.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_timer1.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_timer2.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_timer3.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_uart0.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_uart1.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_uart2.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_uart3.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_usbdev.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_usbhostBase.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_usbhostClass.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_adc.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_clk.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_flash.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_gpio.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_i2c.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/CH59x_lcd.c"	
)

target_include_directories(${lib} 
	PUBLIC 
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc>
	$<INSTALL_INTERFACE:include/>
	$<INSTALL_INTERFACE:include/ch59x/peripheral>
)

# Processor Arch related
target_compile_options(${lib} PUBLIC -msave-restore)

# Optimization. Intentionally kept private.
target_compile_options(${lib} PRIVATE -fmessage-length=0 -fsigned-char -ffunction-sections -fdata-sections -fno-common)
target_compile_options(${lib} PRIVATE -msmall-data-limit=8)
# target_compile_options(${lib_name} PRIVATE -Os)

# Debugging
# target_compile_options(${lib_name} PRIVATE $<$<CONFIG:Debug>:-g>)

# Linker
target_link_options(${lib} PUBLIC -msave-restore)
target_link_directories(${lib}
	PUBLIC
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)
target_link_libraries(${lib}
	PUBLIC
	$<BUILD_INTERFACE:hal::core>
	$<BUILD_INTERFACE:ISP592>
	#$<INSTALL_INTERFACE:hal.core>
)

# set the target's folder (for IDEs that support it, e.g. Visual Studio)
set_target_properties(${lib} PROPERTIES FOLDER "${PROJECT_NAME}")

add_library(hal::peripheral ALIAS ${lib})
