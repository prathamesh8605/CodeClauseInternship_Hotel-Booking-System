import java.util.*;

class Room {
    private int roomNumber;
    private boolean isBooked;

    public Room(int roomNumber) {
        this.roomNumber = roomNumber;
        this.isBooked = false;
    }

    public int getRoomNumber() {
        return roomNumber;
    }

    public boolean isBooked() {
        return isBooked;
    }

    public void book() {
        isBooked = true;
    }

    public void unbook() {
        isBooked = false;
    }
}

class Hotel {
    private String name;
    private Map<Integer, Room> rooms;

    public Hotel(String name) {
        this.name = name;
        this.rooms = new HashMap<>();
    }

    public void addRoom(int roomNumber) {
        if (!rooms.containsKey(roomNumber)) {
            rooms.put(roomNumber, new Room(roomNumber));
        }
    }

    public boolean bookRoom(int roomNumber) {
        Room room = rooms.get(roomNumber);
        if (room != null && !room.isBooked()) {
            room.book();
            return true;
        }
        return false;
    }

    public boolean unbookRoom(int roomNumber) {
        Room room = rooms.get(roomNumber);
        if (room != null && room.isBooked()) {
            room.unbook();
            return true;
        }
        return false;
    }

    public List<Integer> availableRooms() {
        List<Integer> availableRooms = new ArrayList<>();
        for (Map.Entry<Integer, Room> entry : rooms.entrySet()) {
            if (!entry.getValue().isBooked()) {
                availableRooms.add(entry.getKey());
            }
        }
        return availableRooms;
    }
}

public class HotelBookingSystem {
    public static void main(String[] args) {
        Hotel hotel = new Hotel("Example Hotel");

        // Adding rooms to the hotel
        hotel.addRoom(101);
        hotel.addRoom(102);
        hotel.addRoom(103);

        // Booking rooms
        hotel.bookRoom(101);
        hotel.bookRoom(103);

        // Displaying available rooms
        System.out.println("Available rooms: " + hotel.availableRooms());

        // Unbooking a room
        hotel.unbookRoom(101);

        // Displaying available rooms after unbooking
        System.out.println("Available rooms after unbooking: " + hotel.availableRooms());
    }
}
