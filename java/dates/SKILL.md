---
name: dates
description: Handling dates and time in Java
---

# Java Dates y Time (java.time)

## LocalDate (Solo fecha)

```java
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;

// Crear
LocalDate today = LocalDate.now();  // 2025-01-18
LocalDate date = LocalDate.of(2025, 1, 18);
LocalDate fromString = LocalDate.parse("2025-01-18");

// Operaciones
LocalDate tomorrow = today.plusDays(1);
LocalDate yesterday = today.minusDays(1);
LocalDate nextWeek = today.plusWeeks(2);
LocalDate nextMonth = today.plusMonths(1);
LocalDate nextYear = today.plusYears(5);

// Comparaciones
boolean isAfter = today.isAfter(date);
boolean isBefore = today.isBefore(date);
boolean isEqual = today.isEqual(date);
boolean isLeap = today.isLeapYear();

// Días del mes
int dayOfMonth = today.getDayOfMonth();
int dayOfYear = today.getDayOfYear();
int lengthOfMonth = today.lengthOfMonth();
int lengthOfYear = today.lengthOfYear();

// ChronoUnit
long daysBetween = ChronoUnit.DAYS.between(startDate, endDate);
long monthsBetween = ChronoUnit.MONTHS.between(startDate, endDate);

// Transformaciones
LocalDateTime atTime = today.atTime(14, 30);
```

## LocalTime (Solo tiempo)

```java
import java.time.LocalTime;

// Crear
LocalTime now = LocalTime.now();
LocalTime time = LocalTime.of(14, 30, 45);
LocalTime fromString = LocalTime.parse("14:30:45");

// Operaciones
LocalTime later = now.plusHours(2);
LocalTime earlier = now.minusMinutes(30);

// Comparaciones
now.isBefore(time);
now.isAfter(time);

// Componentes
int hour = now.getHour();
int minute = now.getMinute();
int second = now.getSecond();
int nano = now.getNano();

// Truncamiento
LocalTime truncated = now.truncatedTo(ChronoUnit.HOURS);
```

## LocalDateTime (Fecha y tiempo)

```java
import java.time.LocalDateTime;

// Crear
LocalDateTime now = LocalDateTime.now();
LocalDateTime dt = LocalDateTime.of(2025, 1, 18, 14, 30);
LocalDate date = LocalDate.now();
LocalTime time = LocalTime.now();
LocalDateTime combined = date.atTime(time);
LocalTime time2 = LocalTime.now();
LocalDateTime combined2 = date.atTime(time2);

// Extraer componentes
LocalDate datePart = now.toLocalDate();
LocalTime timePart = now.toLocalTime();

// Formateo
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm");
String formatted = now.format(formatter);

// Parsing
LocalDateTime parsed = LocalDateTime.parse("18/01/2025 14:30", formatter);
```

## ZonedDateTime (Con zona horaria)

```java
import java.time.ZonedDateTime;
import java.time.ZoneId;
import java.time.ZoneOffset;

// Crear
ZonedDateTime now = ZonedDateTime.now();
ZonedDateTime withZone = ZonedDateTime.now(ZoneId.of("America/New_York"));
ZonedDateTime withOffset = ZonedDateTime.now(ZoneOffset.of("-05:00"));

// Cambiar zona
ZonedDateTime tokyo = now.withZoneSameInstant(ZoneId.of("Asia/Tokyo"));

// Zone ID
ZoneId zone = ZoneId.systemDefault();
Set<String> zones = ZoneId.getAvailableZoneIds();

// ZonedDateTime específico
ZonedDateTime meeting = ZonedDateTime.of(
    2025, 1, 18, 14, 30, 0, 0,
    ZoneId.of("America/New_York")
);

// Instants
Instant instant = now.toInstant();
Instant fromEpoch = Instant.ofEpochMilli(1705588200000L);
```

## Period y Duration

```java
import java.time.Period;
import java.time.Duration;

// Period (fecha)
Period period = Period.of(2, 3, 10);  // 2 años, 3 meses, 10 días
Period between = Period.between(startDate, endDate);
LocalDate future = today.plus(period);

// Duration (tiempo)
Duration duration = Duration.ofHours(2);
Duration between = Duration.between(startTime, endTime);
LocalTime future = now.plus(duration);

// Parse
Period p = Period.parse("P2Y3M10D");
Duration d = Duration.parse("PT2H30M");

// Componentes
long days = period.getDays();
int months = period.getMonths();
int years = period.getYears();

long hours = duration.toHours();
long minutes = duration.toMinutes();
```

## DateTimeFormatter

```java
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;

// Predefinidos
DateTimeFormatter.ISO_LOCAL_DATE;
DateTimeFormatter.ISO_LOCAL_TIME;
DateTimeFormatter.ISO_LOCAL_DATE_TIME;
DateTimeFormatter.ISO_INSTANT;

// Estilos
DateTimeFormatter formatter = DateTimeFormatter.ofLocalizedDate(FormatStyle.LONG);
String longFormat = now.format(formatter);  // "18 de enero de 2025"

// Patrones
DateTimeFormatter f1 = DateTimeFormatter.ofPattern("dd/MM/yyyy");
DateTimeFormatter f2 = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
DateTimeFormatter f3 = DateTimeFormatter.ofPattern("EEEE, d 'de' MMMM 'de' yyyy");

// Con locale
DateTimeFormatter french = DateTimeFormatter.ofPattern("dd MMMM yyyy", Locale.FRENCH);
```

## Conversiones

```java
// Date → LocalDate
Date date = new Date();
LocalDate localDate = date.toInstant()
    .atZone(ZoneId.systemDefault())
    .toLocalDate();

// LocalDate → Date
Date.from(localDate.atStartOfDay(ZoneId.systemDefault()).toInstant());

// Timestamp → LocalDateTime
long timestamp = System.currentTimeMillis();
LocalDateTime ldt = Instant.ofEpochMilli(timestamp)
    .atZone(ZoneId.systemDefault())
    .toLocalDateTime();

// String → Date (java.util.Date)
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
Date utilDate = sdf.parse("2025-01-18");

// String → LocalDateTime
DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
LocalDateTime ldt = LocalDateTime.parse("2025-01-18T14:30:00");
```

## Formatting para Usuarios

```java
import java.time.format.DateTimeFormatter;

public class DateUtils {
    public static String formatDate(LocalDate date) {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd 'de' MMMM 'de' yyyy", new Locale("es"));
        return date.format(formatter);
    }
    
    public static String formatDateTime(LocalDateTime dateTime) {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm");
        return dateTime.format(formatter);
    }
    
    public static String formatRelative(LocalDate date) {
        LocalDate today = LocalDate.now();
        if (date.isEqual(today)) {
            return "Hoy";
        } else if (date.isEqual(today.plusDays(1))) {
            return "Mañana";
        } else if (date.isEqual(today.minusDays(1))) {
            return "Ayer";
        } else {
            return date.format(DateTimeFormatter.ofPattern("dd/MM/yyyy"));
        }
    }
}
```
