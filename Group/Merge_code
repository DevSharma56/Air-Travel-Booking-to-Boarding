import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.*;

// UserRole enum (Samuel James)
enum UserRole {
    ADMIN, STAFF, CUSTOMER
}

// User class (Samuel James)
class User {
    private String username;
    private UserRole role;

    public User(String username, UserRole role) {
        this.username = username;
        this.role = role;
    }

    public UserRole getRole() { return role; }
}

// Flight class (Dev Sharma + Samuel James)
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
    private String status;

    public Flight(String flightId, String airline, String origin, String destination,
                  LocalDateTime departureTime, LocalDateTime arrivalTime,
                  int capacity, double price, int availableSeats, String status) {
        this.flightId = flightId;
        this.airline = airline;
        this.origin = origin;
        this.destination = destination;
        this.departureTime = departureTime;
        this.arrivalTime = arrivalTime;
        this.capacity = capacity;
        this.price = price;
        this.availableSeats = availableSeats;
        this.status = status;
    }

    public String getFlightId() { return flightId; }
    public String getOrigin() { return origin; }
    public String getDestination() { return destination; }
    public double getPrice() { return price; }
    public int getAvailableSeats() { return availableSeats; }
    public String getStatus() { return status; }
    public void bookSeats(int seats) { if (seats <= availableSeats) availableSeats -= seats; }
    public void updateStatus(String status) { this.status = status; }

    @Override
    public String toString() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
        return "Flight " + flightId + ": " + airline + " from " + origin + " to " + destination + "\n" +
               "Departure: " + departureTime.format(formatter) + " | Arrival: " + arrivalTime.format(formatter) + "\n" +
               "Price: $" + price + " | Available Seats: " + availableSeats + "/" + capacity + " | Status: " + status;
    }
}

// Booking class (Dev Sharma)
class Booking {
    private final String bookingId;
    private final String flightId;
    private final String passengerName;
    private final int seats;
    private final double totalPrice;
    private String paymentStatus;

    public Booking(String bookingId, String flightId, String passengerName, int seats, double totalPrice) {
        this.bookingId = bookingId;
        this.flightId = flightId;
        this.passengerName = passengerName;
        this.seats = seats;
        this.totalPrice = totalPrice;
        this.paymentStatus = "Pending";
    }

    public String getBookingId() { return bookingId; }
    public String getFlightId() { return flightId; }
    public double getTotalPrice() { return totalPrice; }
    public String getPaymentStatus() { return paymentStatus; }
    public void setPaymentStatus(String paymentStatus) { this.paymentStatus = paymentStatus; }

    @Override
    public String toString() {
        return "Booking ID: " + bookingId + "\n" +
               "Flight: " + flightId + "\n" +
               "Passenger: " + passengerName + " | Seats: " + seats + "\n" +
               "Total Price: $" + totalPrice + " | Payment Status: " + paymentStatus;
    }
}

// Passenger class (Adil Hasan)
class Passenger {
    private String passengerId;
    private String name;
    private String bookingReference;
    private boolean checkedIn;
    private String seatNumber;

    public Passenger(String passengerId, String name, String bookingReference) {
        this.passengerId = passengerId;
        this.name = name;
        this.bookingReference = bookingReference;
        this.checkedIn = false;
        this.seatNumber = "Not Assigned";
    }

    public String getBookingReference() { return bookingReference; }
    public boolean isCheckedIn() { return checkedIn; }
    public String getSeatNumber() { return seatNumber; }
    public void checkIn(String seatNumber) {
        this.checkedIn = true;
        this.seatNumber = seatNumber;
    }

    public void displayPassengerDetails() {
        System.out.println("Passenger: " + name);
        System.out.println("Booking Reference: " + bookingReference);
        System.out.println("Checked-In: " + (checkedIn ? "Yes" : "No"));
        System.out.println("Seat Number: " + seatNumber);
    }
}

// Transaction class (Annup Kumar)
class Transaction {
    private String transactionId;
    private double amount;
    private String status;

    public Transaction(String transactionId, double amount) {
        this.transactionId = transactionId;
        this.amount = amount;
        this.status = "Success";
    }

    public String getTransactionId() { return transactionId; }
    public double getAmount() { return amount; }
    public String getStatus() { return status; }
    public void setStatus(String status) { this.status = status; }

    public void printReceipt() {
        System.out.println("\n🧾 Payment Receipt");
        System.out.println("------------------------------");
        System.out.println("Transaction ID: " + transactionId);
        System.out.println("Amount Paid: $" + amount);
        System.out.println("Payment Status: " + status);
        System.out.println("------------------------------\n");
    }
}

// PaymentGateway abstract class (Annup Kumar)
abstract class PaymentGateway {
    protected String gatewayName;

    public PaymentGateway(String gatewayName) {
        this.gatewayName = gatewayName;
    }

    public abstract boolean processPayment(double amount, String transactionId);
    public abstract boolean refundPayment(String transactionId, double amount);
}

// StripeGateway class (Annup Kumar)
class StripeGateway extends PaymentGateway {
    public StripeGateway() {
        super("Stripe");
    }

    @Override
    public boolean processPayment(double amount, String transactionId) {
        System.out.println("✅ Payment of $" + amount + " successfully processed via " + gatewayName);
        return true;
    }

    @Override
    public boolean refundPayment(String transactionId, double amount) {
        System.out.println("🔄 Refunding $" + amount + " via " + gatewayName);
        return true;
    }
}

// PayPalGateway class (Annup Kumar)
class PayPalGateway extends PaymentGateway {
    public PayPalGateway() {
        super("PayPal");
    }

    @Override
    public boolean processPayment(double amount, String transactionId) {
        System.out.println("✅ Payment of $" + amount + " successfully processed via " + gatewayName);
        return true;
    }

    @Override
    public boolean refundPayment(String transactionId, double amount) {
        System.out.println("🔄 Refunding $" + amount + " via " + gatewayName);
        return true;
    }
}

// AirlineData class (Central data management)
class AirlineData {
    private Map<String, Flight> flights = new HashMap<>();
    private Map<String, Booking> bookings = new HashMap<>();
    private Map<String, Passenger> passengers = new HashMap<>();
    private Map<String, Transaction> transactions = new HashMap<>();
    private List<User> users = new ArrayList<>();

    public void addFlight(Flight flight) { flights.put(flight.getFlightId(), flight); }
    public Flight getFlight(String flightId) { return flights.get(flightId); }
    public List<Flight> getAllFlights() { return new ArrayList<>(flights.values()); }
    public void addBooking(Booking booking) { bookings.put(booking.getBookingId(), booking); }
    public Booking getBooking(String bookingId) { return bookings.get(bookingId); }
    public List<Booking> getAllBookings() { return new ArrayList<>(bookings.values()); }
    public void addPassenger(Passenger passenger) { passengers.put(passenger.getBookingReference(), passenger); }
    public Passenger getPassenger(String bookingReference) { return passengers.get(bookingReference); }
    public void addTransaction(Transaction transaction) { transactions.put(transaction.getTransactionId(), transaction); }
    public void addUser(User user) { users.add(user); }
}

// FlightSystem class (Dev Sharma)
class FlightSystem {
    private AirlineData data;
    private Random random = new Random();

    public FlightSystem(AirlineData data) {
        this.data = data;
    }

    public List<Flight> searchFlights(String origin, String destination) {
        List<Flight> results = new ArrayList<>();
        for (Flight flight : data.getAllFlights()) {
            if (flight.getOrigin().equalsIgnoreCase(origin) &&
                flight.getDestination().equalsIgnoreCase(destination)) {
                results.add(flight);
            }
        }
        return results;
    }

    public Booking bookFlight(String flightId, String passengerName, int seats) {
        Flight flight = data.getFlight(flightId);
        if (flight == null || seats > flight.getAvailableSeats()) {
            System.out.println("Flight not found or insufficient seats.");
            return null;
        }
        String bookingId = "B" + random.nextInt(10000);
        double totalPrice = seats * flight.getPrice();
        Booking booking = new Booking(bookingId, flightId, passengerName, seats, totalPrice);
        flight.bookSeats(seats);
        data.addBooking(booking);
        data.addPassenger(new Passenger("P" + random.nextInt(10000), passengerName, bookingId));
        return booking;
    }
}

// CheckInSystem class (Adil Hasan)
class CheckInSystem {
    private AirlineData airlineDatabase;
    private List<String> availableSeats;

    public CheckInSystem(AirlineData airlineDatabase) {
        this.airlineDatabase = airlineDatabase;
        this.availableSeats = new ArrayList<>(Arrays.asList("1A", "1B", "2A", "2B", "3A", "3B"));
    }

    public void checkInPassenger(String bookingReference) {
        Passenger passenger = airlineDatabase.getPassenger(bookingReference);
        if (passenger == null) {
            System.out.println("Error: Booking Reference Not Found!");
            return;
        }
        if (passenger.isCheckedIn()) {
            System.out.println("Passenger already checked in.");
            return;
        }
        System.out.println("Available Seats: " + availableSeats);
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter seat number to select: ");
        String chosenSeat = scanner.nextLine();
        if (!availableSeats.contains(chosenSeat)) {
            System.out.println("Invalid Seat Selection! Try Again.");
            return;
        }
        passenger.checkIn(chosenSeat);
        availableSeats.remove(chosenSeat);
        System.out.println("Check-in Successful! Boarding Pass Generated.\n");
        passenger.displayPassengerDetails();
    }
}

// PaymentProcessor class (Annup Kumar)
class PaymentProcessor {
    private PaymentGateway paymentGateway;
    private AirlineData data;

    public PaymentProcessor(PaymentGateway paymentGateway, AirlineData data) {
        this.paymentGateway = paymentGateway;
        this.data = data;
    }

    public String makePayment(String bookingId) {
        Booking booking = data.getBooking(bookingId);
        if (booking == null) {
            System.out.println("Booking not found.");
            return null;
        }
        if (!booking.getPaymentStatus().equals("Pending")) {
            System.out.println("Payment already processed.");
            return null;
        }
        String transactionId = "TXN" + System.currentTimeMillis();
        Transaction transaction = new Transaction(transactionId, booking.getTotalPrice());
        if (paymentGateway.processPayment(booking.getTotalPrice(), transactionId)) {
            booking.setPaymentStatus("Paid");
            data.addTransaction(transaction);
            transaction.printReceipt();
            return transactionId;
        } else {
            System.out.println("❌ Payment Failed.");
            return null;
        }
    }
}

// SystemAdmin class (Samuel James)
class SystemAdmin {
    private AirlineData data;

    public SystemAdmin(AirlineData data) {
        this.data = data;
    }

    public void addFlight(String flightId, String airline, String origin, String destination,
                          LocalDateTime departureTime, LocalDateTime arrivalTime,
                          int capacity, double price, int availableSeats, String status) {
        Flight flight = new Flight(flightId, airline, origin, destination, departureTime, arrivalTime,
                                   capacity, price, availableSeats, status);
        data.addFlight(flight);
        System.out.println("Flight added: " + flightId);
    }

    public void updateFlightStatus(String flightId, String newStatus) {
        Flight flight = data.getFlight(flightId);
        if (flight != null) {
            flight.updateStatus(newStatus);
            System.out.println("Updated: " + flight);
        } else {
            System.out.println("Flight not found.");
        }
    }

    public void displayFlights() {
        for (Flight flight : data.getAllFlights()) {
            System.out.println(flight);
        }
    }

    public void displayBookings() {
        for (Booking booking : data.getAllBookings()) {
            System.out.println(booking);
        }
    }
}

// Main class integrating all components
public class AirlineBookingSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        AirlineData data = new AirlineData();
        FlightSystem flightSystem = new FlightSystem(data);
        CheckInSystem checkInSystem = new CheckInSystem(data);
        SystemAdmin admin = new SystemAdmin(data);

        // Initialize sample data
        data.addFlight(new Flight("F101", "Airline A", "CityA", "CityB",
                LocalDateTime.now().plusDays(1), LocalDateTime.now().plusDays(1).plusHours(3),
                200, 300, 200, "Scheduled"));
        data.addFlight(new Flight("F102", "Airline B", "CityA", "CityC",
                LocalDateTime.now().plusDays(2), LocalDateTime.now().plusDays(2).plusHours(4),
                150, 250, 150, "Scheduled"));

        while (true) {
            System.out.println("\n==== AIRLINE BOOKING SYSTEM ====");
            System.out.println("1. Admin Menu");
            System.out.println("2. Passenger Menu");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            if (choice == 1) {
                adminMenu(admin, scanner);
            } else if (choice == 2) {
                passengerMenu(flightSystem, checkInSystem, data, scanner);
            } else if (choice == 3) {
                System.out.println("Exiting system. Goodbye!");
                break;
            } else {
                System.out.println("Invalid choice.");
            }
        }
        scanner.close();
    }

    private static void adminMenu(SystemAdmin admin, Scanner scanner) {
        while (true) {
            System.out.println("\n==== ADMIN MENU ====");
            System.out.println("1. Add Flight");
            System.out.println("2. Update Flight Status");
            System.out.println("3. Display Flights");
            System.out.println("4. Display Bookings");
            System.out.println("5. Back");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    System.out.print("Enter Flight ID: ");
                    String flightId = scanner.nextLine();
                    System.out.print("Enter Airline: ");
                    String airline = scanner.nextLine();
                    System.out.print("Enter Origin: ");
                    String origin = scanner.nextLine();
                    System.out.print("Enter Destination: ");
                    String destination = scanner.nextLine();
                    System.out.print("Enter Capacity: ");
                    int capacity = scanner.nextInt();
                    System.out.print("Enter Price: ");
                    double price = scanner.nextDouble();
                    scanner.nextLine();
                    admin.addFlight(flightId, airline, origin, destination,
                            LocalDateTime.now().plusDays(1), LocalDateTime.now().plusDays(1).plusHours(3),
                            capacity, price, capacity, "Scheduled");
                    break;
                case 2:
                    System.out.print("Enter Flight ID: ");
                    String flightNum = scanner.nextLine();
                    System.out.print("Enter New Status: ");
                    String newStatus = scanner.nextLine();
                    admin.updateFlightStatus(flightNum, newStatus);
                    break;
                case 3:
                    admin.displayFlights();
                    break;
                case 4:
                    admin.displayBookings();
                    break;
                case 5:
                    return;
                default:
                    System.out.println("Invalid choice.");
            }
        }
    }

    private static void passengerMenu(FlightSystem flightSystem, CheckInSystem checkInSystem,
                                      AirlineData data, Scanner scanner) {
        System.out.println("Select Payment Method:");
        System.out.println("1. Stripe");
        System.out.println("2. PayPal");
        System.out.print("Enter choice (1/2): ");
        int paymentChoice = scanner.nextInt();
        scanner.nextLine();
        PaymentGateway gateway = (paymentChoice == 1) ? new StripeGateway() : new PayPalGateway();
        PaymentProcessor paymentProcessor = new PaymentProcessor(gateway, data);

        while (true) {
            System.out.println("\n==== PASSENGER MENU ====");
            System.out.println("1. Search Flights");
            System.out.println("2. Book Flight");
            System.out.println("3. Make Payment");
            System.out.println("4. Check-in");
            System.out.println("5. Back");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    System.out.print("Enter origin city: ");
                    String origin = scanner.nextLine();
                    System.out.print("Enter destination city: ");
                    String destination = scanner.nextLine();
                    List<Flight> flights = flightSystem.searchFlights(origin, destination);
                    flights.forEach(System.out::println);
                    break;
                case 2:
                    System.out.print("Enter Flight ID: ");
                    String flightId = scanner.nextLine();
                    System.out.print("Enter Passenger Name: ");
                    String passengerName = scanner.nextLine();
                    System.out.print("Enter Number of Seats: ");
                    int seats = scanner.nextInt();
                    scanner.nextLine();
                    Booking booking = flightSystem.bookFlight(flightId, passengerName, seats);
                    if (booking != null) System.out.println(booking);
                    break;
                case 3:
                    System.out.print("Enter Booking ID: ");
                    String bookingId = scanner.nextLine();
                    paymentProcessor.makePayment(bookingId);
                    break;
                case 4:
                    System.out.print("Enter Booking Reference: ");
                    String bookingRef = scanner.nextLine();
                    checkInSystem.checkInPassenger(bookingRef);
                    break;
                case 5:
                    return;
                default:
                    System.out.println("Invalid choice.");
            }
        }
    }
}
