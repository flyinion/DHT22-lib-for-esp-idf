# DHT22 / AM2302 C/C++ Component for ESP32 (ESP-IDF)

This is an ESP32 C/C++ (esp-idf) library for the DHT22 low cost temperature/humidity sensors.

Forked from https://github.com/Andrey-m/DHT22-lib-for-esp-idf, which was in turn forked from https://github.com/gosouth/DHT22 and https://github.com/gosouth/DHT22-cpp.

I added `CMakeLists.txt` and `idf_component.yml` files to more easily incorporate it in `esp-idf` projects.

I also added tests and made the examples buildable in `esp-idf`.

## Tests

To build and run firmware (integration) tests: 

```sh
$ cd fwtest
$ idf.py set-target esp32
...
$ idf.py -p /dev/ttyUSB0 flash monitor
...
```

## Examples

See the example code below, or in repo [in C](https://github.com/flyinion/DHT22-lib-for-esp-idf/blob/master/examples/C/main/main.c) or [in C++](https://github.com/flyinion/DHT22-lib-for-esp-idf/blob/master/examples/CPP/main/main.cpp). 

Edit the code if necessary to set the correct GPIO pin to which you have wired your DHT sensor.

To build and run and monitor:

```sh
$ cd examples/C
$ idf.py set-target esp32
...
$ idf.py -p /dev/ttyUSB0 flash monitor
...
```

## Use in C

See [example code in C](https://github.com/flyinion/DHT22-lib-for-esp-idf/blob/master/examples/C/main/main.c).

```C
void DHT_task(void *pvParameter)
{
    setDHTgpio(GPIO_NUM_4);
    ESP_LOGI(TAG, "Starting DHT Task\n\n");

    while (1)
    {
        ESP_LOGI(TAG, "=== Reading DHT ===\n");
        int ret = readDHT();

        errorHandler(ret);

        ESP_LOGI(TAG, "Hum: %.1f Tmp: %.1f\n", getHumidity(), getTemperature())

        // -- wait at least 3 sec before reading again ------------
        // The interval of whole process must be beyond 2 seconds !!
        vTaskDelay(3000 / portTICK_RATE_MS);
    }
}

void app_main()
{
    //Initialize NVS
    esp_err_t ret = nvs_flash_init();
    if (ret == ESP_ERR_NVS_NO_FREE_PAGES)
    {
        ESP_ERROR_CHECK(nvs_flash_erase());
        ret = nvs_flash_init();
    }
    ESP_ERROR_CHECK(ret);

    esp_log_level_set("*", ESP_LOG_INFO);

    xTaskCreate(&DHT_task, "DHT_task", 2048, NULL, 5, NULL);
}
```
## Use in C++

See [example code in C++](https://github.com/flyinion/DHT22-lib-for-esp-idf/blob/master/examples/CPP/main/main.cpp).

```C
void DHT_task(void *pvParameter)
{
    DHT dht;
    dht.setDHTgpio(GPIO_NUM_4);
    ESP_LOGI(TAG, "Starting DHT Task\n\n");

    while (1)
    {
        ESP_LOGI(TAG, "=== Reading DHT ===\n");
        int ret = dht.readDHT();

        dht.errorHandler(ret);

        ESP_LOGI(TAG, "Hum: %.1f Tmp: %.1f\n", dht.getHumidity(), dht.getTemperature())

        // -- wait at least 3 sec before reading again ------------
        // The interval of whole process must be beyond 2 seconds !!
        vTaskDelay(3000 / portTICK_RATE_MS);
    }
}

void app_main()
{
    //Initialize NVS
    esp_err_t ret = nvs_flash_init();
    if (ret == ESP_ERR_NVS_NO_FREE_PAGES)
    {
        ESP_ERROR_CHECK(nvs_flash_erase());
        ret = nvs_flash_init();
    }
    ESP_ERROR_CHECK(ret);

    esp_log_level_set("*", ESP_LOG_INFO);

    xTaskCreate(&DHT_task, "DHT_task", 2048, NULL, 5, NULL);
}
```

## Incorporate in ESP-IDF as a Dependency

Example how to specify your project's `main/idf_component.yml` file in order to use it as a dependency:

```
version: "1.0.0"
targets:
  - esp32
description: DDNet Ambient Sensor
url: https://github.com/flyinion/ambient
dependencies:
  idf: ">=4.1"
  DHT22-lib-for-esp-idf: 
    version: "1.0.0"
    # path: /home/jmfife/projects/DHT22-lib-for-esp-idf
    git: ssh://github.com/flyinion/DHT22-lib-for-esp-idf.git
```
