import java.time.LocalDate; 
import java.time.format.DateTimeFormatter; 
import java.time.format.DateTimeParseException; 
import java.time.temporal.ChronoUnit; 
import java.util.Scanner; 
 
public class Main { 
    public static void main(String[] args) { 
        Scanner scanner = new Scanner(System.in); 
 
        while (true) { 
            System.out.println("Введите дату рождения в формате ДД.MM.ГГГГ:"); 
            String inputDate = scanner.nextLine(); 
 
            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd.MM.yyyy"); 
            try { 
                LocalDate birthdate = LocalDate.parse(inputDate, formatter); 
                LocalDate today = LocalDate.now(); 
                long years = ChronoUnit.YEARS.between(birthdate, today); 
                long months = ChronoUnit.MONTHS.between(birthdate, today) % 12; 
                long days = ChronoUnit.DAYS.between(birthdate, today) % 30;  
                LocalDate nextBirthday = birthdate.withYear(today.getYear()); 
                if (nextBirthday.isBefore(today) || nextBirthday.isEqual(today)) { 
                    nextBirthday = nextBirthday.plusYears(1); 
                } 
                long daysLeft = ChronoUnit.DAYS.between(today, nextBirthday); 
                String dayOfWeek = birthdate.getDayOfWeek().toString(); 
 
                System.out.println("Возраст: " + years + " лет, " + months + " месяцев, " + days + " дней"); 
                System.out.println("Дней до следующего дня рождения: " + daysLeft + " дней"); 
                System.out.println("Дата следующего дня рождения: " + nextBirthday.format(formatter)); 
                System.out.println("День недели дня рождения: " + dayOfWeek); 
                break; 
            } catch (DateTimeParseException e) { 
                System.out.println("Ошибка при вводе даты. Пожалуйста, введите дату в корректном формате."); 
            } 
        } 
        scanner.close(); 
    } 
}
