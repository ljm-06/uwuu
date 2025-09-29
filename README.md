import java.util.PriorityQueue;

class Patient implements Comparable<Patient> {
    String name;
    int priority;
    String condition;
    String arrivalTime;

    public Patient(String name, int priority, String condition, String arrivalTime) {
        this.name = name;
        this.priority = priority;
        this.condition = condition;
        this.arrivalTime = arrivalTime;
    }

    public int compareTo(Patient other) {
        if (this.priority != other.priority) {
            return this.priority - other.priority; // smaller number means higher priority
        } else {
            return this.arrivalTime.compareTo(other.arrivalTime); // earlier time first
        }
    }

    public String toString() {
        return "[P" + priority + "] " + name + " - " + condition + " (" + arrivalTime + ")";
    }
}

class ERQueue {
    PriorityQueue<Patient> queue = new PriorityQueue<>();

    public void arrive(String name, int priority, String condition, String time) {
        Patient p = new Patient(name, priority, condition, time);
        queue.add(p);
    }

    public void treatNext() {
        System.out.println(">>> Treating patient now...");
        Patient p = queue.poll();
        if (p != null) {
            System.out.println("Treated: " + p);
        } else {
            System.out.println("No patients left.");
        }
    }

    public void displayQueue() {
        System.out.println("\n=== UPDATED QUEUE ===");
        System.out.println("Patients Waiting: " + queue.size());

        int i = 1;
        for (Patient p : queue) {
            System.out.println(i + ". " + p);
            i++;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        ERQueue er = new ERQueue();

        er.arrive("Pedro Cruz", 1, "Head injury - NOW UNCONSCIOUS ⚠️", "23:52");
        er.arrive("Carlos Mendoza", 2, "Compound fracture - leg", "23:50");
        er.arrive("Lisa Wang", 2, "Severe asthma attack", "23:56");
        er.arrive("Maria Santos", 3, "Deep laceration on arm", "23:48");
        er.arrive("Ana Lim", 4, "Sprained ankle", "23:49");

        er.displayQueue();
        er.treatNext();
        er.displayQueue();
    }
}
