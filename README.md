graph TD;
    subgraph System_Logic [System Logic]
        Start([Start]) --> Read_Sensor[Read Analog Sensor];
        Read_Sensor --> Check{Turbidity > 20?};
        Check -- Yes (Dirty) --> LED_Red[Turn ON Red LED];
        Check -- No (Clean) --> LED_Green[Turn ON Green LED];
        LED_Red --> Serial[Print 'Unsafe' to Serial];
        LED_Green --> Serial;
    end

    subgraph Hardware_Connections [Wiring]
        ESP32[ESP32 DevKit V1] ---|GPIO 34| Sensor(Turbidity Sensor);
        ESP32 ---|GPIO 2| LED_G(Green LED);
        ESP32 ---|GPIO 4| LED_R(Red LED);
        ESP32 ---|USB| PC(Computer);
    end

    style ESP32 fill:#f9f,stroke:#333,stroke-width:2px
    style Sensor fill:#ccf,stroke:#333
