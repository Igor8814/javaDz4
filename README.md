```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Scanner;

public class program4 {
    public static void main(String[] args) {
        List<String> listNames = new ArrayList<>();
        List<String> listSurnames = new ArrayList<>();
        List<String> listMidNames = new ArrayList<>();
        List<Integer> listAges = new ArrayList<>();
        List<Boolean> listSexes = new ArrayList<>();
        List<Integer> keys = new LinkedList<>();
        boolean flag = true;
        int listSize = 0;
        while (flag) {
            try (Scanner scanner = new Scanner(System.in)) {
                System.out.print("Введите свое имя, фамилию, отчество: ");
                String fio = scanner.nextLine();
                String[] fio1 = fio.split(" ");
                if (fio1.length == 3) {
                    listNames.add(fio1[0]);
                    listSurnames.add(fio1[1]);
                    listMidNames.add(fio1[2]);
                } else if (fio1.length == 2) {
                    listNames.add(fio1[0]);
                    listSurnames.add(fio1[1]);
                    listMidNames.add("");
                } else {
                    listNames.add(fio1[0]);
                    listSurnames.add("");
                    listMidNames.add("");
                }
            }
            boolean isAge = true;
            System.out.print("Введите свой возраст: ");
            while (isAge) {
                try {
                    try (Scanner scanner_age = new Scanner(System.in)) {
                        Integer age = scanner_age.nextInt();
                        listAges.add(age);
                    }
                    isAge = false;
                } catch (Exception e) {
                    System.out.print("Пожалуйста, введите целое число! Введите свой возраст: ");
                }
            }
            try (Scanner scanner_sex = new Scanner(System.in)) {
                System.out.print("Пожалуйста, введите пол (М или Ж): ");
                if (scanner_sex.next().toUpperCase().contains("М")) {
                    listSexes.add(true);
                } else
                    listSexes.add(false);
            }
            keys.add(listAges.size() - 1);
            System.out.println("Вы хотите ввести следующий? Y/N");
            try (Scanner scanner1 = new Scanner(System.in)) {
                String yn = scanner1.nextLine();
                if (yn.toUpperCase().equals("N"))
                    flag = false;
            }
        }

        System.out.println("Вы ввели всех лиц");

        keys = sortByAge(listAges, keys);
        listSize = listAges.size();
        for (int i : keys) {
            listNames.add(listNames.get(i));
            listSurnames.add(listSurnames.get(i));
            listMidNames.add(listMidNames.get(i));
            listSexes.add(listSexes.get(i));
            listAges.add(listAges.get(i));
        }
        System.out.println("listSize = " + listSize);
        
        for (int i = 0; i < listSize; i++) {
            listNames.remove(0);
            listSurnames.remove(0);
            listMidNames.remove(0);;
            listSexes.remove(0);
            listAges.remove(0);
                        
        }

        System.out.println(listNames);
        System.out.println(listSurnames);
        System.out.println(listMidNames);
        System.out.println(listAges);
        System.out.println(listSexes);

       

    }

    static List<Integer> sortByAge(List<Integer> listAges, List<Integer> keys) {
        System.out.println("Сортировать по возрасту:");

        int cnt = listAges.size() - 1;
        while (cnt >= 0) {
            int maxAge = listAges.get(keys.get(cnt));
            int index = cnt;
            for (int i = 0; i < cnt; i++) {
                if (maxAge < listAges.get(keys.get(i))) {
                    maxAge = listAges.get(keys.get(i));
                    index = i;
                }
            }
            int tmp = keys.get(cnt);
            keys.set(cnt, keys.get(index));
            keys.set(index, tmp);
            cnt--;
        }
        System.out.println("Keys: " + keys);
        return keys;
    }
}
```
