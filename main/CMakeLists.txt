idf_component_register(SRCS "app_main.c"
                    PRIV_REQUIRES mqtt nvs_flash esp_netif esp_driver_gpio
                    INCLUDE_DIRS ".")
