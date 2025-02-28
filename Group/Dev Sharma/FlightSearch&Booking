import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.*;

class Flight {
    private final String flightId;
    private final String airline;
    private final String origin;
    private final String destination;
    private final LocalDateTime departureTime;
    private final LocalDateTime arrivalTime;
    private final int capacity;
    private final double price;
    private int availableSeats;

    public Flight(String flightId, String airline, String origin, String destination,
                  LocalDateTime departureTime, LocalDateTime arrivalTime,
                  int capacity, double price, int availableSeats) {
        this.flightId = flightId;
        this.airline = airline;
        this.origin = origin;
        this.destination = destination;
        this.departureTime = departureTime;
        this.arrivalTime = arrivalTime;
        this.capacity = capacity;
        this.price = price;
        this.availableSeats = availableSeats;
    }

    public String getFlightId() { return flightId; }
    public String getOrigin() { return origin; }
    public String getDestination() { return destination; }
    public LocalDateTime getDepartureTime() { return departureTime; }
    public double getPrice() { return price; }
    public int getAvailableSeats() { return availableSeats; }
    public void bookSeats(int seats) { if (seats <= availableSeats) availableSeats -= seats; }
    public void cancelSeats(int seats) { if (seats > 0) availableSeats += seats; }

    @Override
    public String toString() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
        return "Flight " + flightId + ": " + airline + " from " + origin + " to " + destination + "\n" +
               "Departure: " + departureTime.format(formatter) + " | Arrival: " + arrivalTime.format(formatter) + "\n" +
               "Price: $" + price + " | Available Seats: " + availableSeats + "/" + capacity;
    }
}

class Booking {
    private final String bookingId;
    private final String flightId;
    private final String passengerName;
    private final int seats;
    private final double totalPrice;

    public Booking(String bookingId, String flightId, String passengerName, int seats, double totalPrice) {
        this.bookingId = bookingId;
        this.flightId = flightId;
        this.passengerName = passengerName;
        this.seats = seats;
        this.totalPrice = totalPrice;
    }

    public String getBookingId() { return bookingId; }
    public String getFlightId() { return flightId; }

    @Override
    public String toString() {
        return "Booking ID: " + bookingId + "\n" +
               "Flight: " + flightId + "\n" +
               "Passenger: " + passengerName + " | Seats: " + seats + "\n" +
               "Total Price: $" + totalPrice;
    }
}

class FlightSystem {
    private final Map<String, Flight> flights = new HashMap<>();
    private final Map<String, Booking> bookings = new HashMap<>();
    private final Random random = new Random();

    public void addSampleFlights() {
        for (int i = 1; i <= 10; i++) {
            flights.put("F10" + i, new Flight("F10" + i, "Airline " + i, "CityA", "CityB",
                    LocalDateTime.now().plusDays(i), LocalDateTime.now().plusDays(i).plusHours(3),
                    200, 300 + (i * 50), 200));
        }
    }

    public void addSampleBookings() {
        for (int i = 1; i <= 10; i++) {
            bookings.put("B10" + i, new Booking("B10" + i, "F10" + (i % 10 + 1), "Passenger " + i, i, (300 + (i * 50)) * i));
        }
    }

    public List<Flight> searchFlights(String origin, String destination) {
        List<Flight> results = new ArrayList<>();
        for (Flight flight : flights.values()) {
            if (flight.getOrigin().equalsIgnoreCase(origin) &&
                flight.getDestination().equalsIgnoreCase(destination)) {
                results.add(flight);
            }
        }
        return results;
    }

    public Flight getFlight(String flightId) {
        return flights.get(flightId);
    }

    public Booking getBooking(String bookingId) {
        return bookings.get(bookingId);
    }
}

public class FlightBookingSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        FlightSystem system = new FlightSystem();
        system.addSampleFlights();
        system.addSampleBookings();
        
        while (true) {
            System.out.println("\n==== FLIGHT SEARCH & BOOKING SYSTEM ====");
            System.out.println("1. Search Flights");
            System.out.println("2. View Flight Details");
            System.out.println("3. View Booking Details");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1 -> {
                    System.out.print("Enter origin city: ");
                    String origin = scanner.nextLine();
                    System.out.print("Enter destination city: ");
                    String destination = scanner.nextLine();
                    List<Flight> flights = system.searchFlights(origin, destination);
                    flights.forEach(System.out::println);
                }
                case 2 -> {
                    System.out.print("Enter Flight ID: ");
                    String flightId = scanner.nextLine();
                    Flight flight = system.getFlight(flightId);
                    System.out.println(flight != null ? flight : "Flight not found.");
                }
                case 3 -> {
                    System.out.print("Enter Booking ID: ");
                    String bookingId = scanner.nextLine();
                    Booking booking = system.getBooking(bookingId);
                    System.out.println(booking != null ? booking : "Booking not found.");
                }
                case 4 -> {
                    System.out.println("Exiting system. Goodbye!");
                    scanner.close();
                    return;
                }
            }
        }
    }
}
