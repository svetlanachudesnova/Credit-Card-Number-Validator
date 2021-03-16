# Отчёт о тестировании Credit Card Number Validator #
## Краткое описание
16.03.2021 было проведено функциональное тестирование приложения Credit Card Number Validator.

На тестирование затрачено: 2 ч

В результате тестирования выявлены следующие дефекты:

* [Валидные номера карт не проходят проверку](https://github.com/svetlanachudesnova/Credit-Card-Number-Validator/issues/1)

## Описание процесса тестирования
В процессе тестирования тестировались следующие артефакты:
* [Руководство по установке IntelliJ IDEA](https://github.com/netology-code/javaqa-homeworks/blob/master/intro/idea.md)
* Код приложения 
 ```java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```

В качестве тестовых данных использовались данные с [генератора валидных номеров карт:](https://www.freeformatter.com/credit-card-number-generator-validator.html)

* **VISA:**
<br>4916358172241710
<br>4485545916339013
<br>4485170446222561464
* **MasterCard:**
<br>2720995192269484
<br>2720992808760881
<br>5315377277549433
* **American Express (AMEX):**
<br>341893089753020
<br>373269298778424
<br>349362904465998
* **Discover:**
<br>6011777734626937
<br>6011015543776274
<br>6011590507216098682
* **JCB:**
<br>3544322047093237
<br>3541086430445709
<br>3530420034510218377
* **Diners Club - North America:**
<br>5574232932282217
<br>5480501514505986
<br>5456620340386534
* **Diners Club - Carte Blanche:**
<br>30119356783037
<br>30234714482105
<br>30410912587198
* **Diners Club - International:**
<br>36995135302452
<br>36002369649193
<br>36532935249284
* **Maestro:**
<br>6763728912545373
<br>5020215866104838
<br>5038207452644830
* **Visa Electron:**
<br>4175003942314514
<br>4175007086242449
<br>4913886126213685
* **InstaPayment:**
<br>6373093944297994
<br>6391846783575384
<br>6381146200770755

**Тестирование производилось в следующем окружении:**
* Windows 10 Pro 20H2 x64
* jdk-11.0.5+10
* IntelliJ IDEA Communiity Edition