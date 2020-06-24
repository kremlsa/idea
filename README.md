# idea
idea
k
l
package phonebook;
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;

import static java.util.Collections.binarySearch;

class ReadFile {
    public static ArrayList<String> read(String filepath) {
        ArrayList<String> arr = new ArrayList<String>();
        try {
            File myFile = new File(filepath);
            FileReader fileReader = new FileReader(myFile);
            BufferedReader reader = new BufferedReader(fileReader);
            String line = null;
            while ((line = reader.readLine()) != null) {
                arr.add(line);
            }
            reader.close();
        } catch (Exception ex) {
            ex.printStackTrace();
        }
        return arr;
    }
}

class SearchMenu {
    ArrayList<String> personsToFind = new ArrayList<String>();
    ArrayList<String> phoneBook = new ArrayList<String>();
    ArrayList<String> sortedBook = new ArrayList<String>();
    long elapsedTimeB;
    long elapsedTime;
    long elapsedTimeJ;
    long elapsedTimeQ;
    long elapsedTimeBin;
    int count = 0;
    int countJ = 0;
    int countBin = 0;
    public void run() {
        String filepath = "C:\\Java_lessons\\find.txt";
        String filepath2 = "C:\\Java_lessons\\directory1.txt";
        personsToFind = ReadFile.read(filepath);
        phoneBook = ReadFile.read(filepath2);
        linearSearch();
        int seconds = (int) (elapsedTime / 1000) % 60;
        int minutes = (int) ((elapsedTime / (1000*60)) % 60);
        int miliseconds   = (int) (elapsedTime % 1000);
        System.out.println("Start searching (linear search)...");
        System.out.println("Found " + count + " / " + personsToFind.size() + " entries. " +
                "Time taken: " + minutes + " min. " + seconds + " sec. " + miliseconds + " ms.");
        System.out.println();
       /* boolean isSort = bubbleSort();
        if (isSort == true) {
            for (String s : personsToFind) {
                if (jumpSearch(s) >= 0) {
                    countJ++;
                }
            }

        } else {
            linearSearch();
        }
        System.out.println("Start searching (bubble sort + jump search)...");


        if (isSort == true) {
            long elapsedTimeT = elapsedTimeJ + elapsedTimeB;
            seconds = (int) (elapsedTimeT / 1000) % 60;
            minutes = (int) ((elapsedTimeT / (1000*60)) % 60);
            miliseconds   = (int) (elapsedTimeT % 1000);
            System.out.println("Found " + countJ + " / " + personsToFind.size() + " entries. " +
                    "Time taken: " + minutes + " min. " + seconds + " sec. " + miliseconds + " ms.");
            seconds = (int) (elapsedTimeB / 1000) % 60;
            minutes = (int) ((elapsedTimeB / (1000*60)) % 60);
            miliseconds   = (int) (elapsedTimeB % 1000);
            System.out.println("Sorting time: " +
                    minutes + " min. " + seconds + " sec. " + miliseconds + " ms.");
            seconds = (int) (elapsedTimeJ / 1000) % 60;
            minutes = (int) ((elapsedTimeJ / (1000*60)) % 60);
            miliseconds   = (int) (elapsedTimeJ % 1000);
            System.out.println("Searching time: " +
                    minutes + " min. " + seconds + " sec. " + miliseconds + " ms.");
        } else {
            long elapsedTimeT = elapsedTime + elapsedTimeB;
            seconds = (int) (elapsedTimeT / 1000) % 60;
            minutes = (int) ((elapsedTimeT / (1000*60)) % 60);
            miliseconds   = (int) (elapsedTimeT % 1000);
            System.out.println("Found " + count + " / " + personsToFind.size() + " entries. " +
                    "Time taken: " + minutes + " min. " + seconds + " sec. " + miliseconds + " ms.");
            seconds = (int) (elapsedTimeB / 1000) % 60;
            minutes = (int) ((elapsedTimeB / (1000*60)) % 60);
            miliseconds   = (int) (elapsedTimeB % 1000);
            System.out.println("Sorting time: " +
                    minutes + " min. " + seconds + " sec. " + miliseconds + " ms." +
                    " - STOPPED, moved to linear search");
            seconds = (int) (elapsedTime / 1000) % 60;
            minutes = (int) ((elapsedTime / (1000*60)) % 60);
            miliseconds   = (int) (elapsedTime % 1000);
            System.out.println("Searching time: " +
                    minutes + " min. " + seconds + " sec. " + miliseconds + " ms.");

        }*/

        //personsToFind = ReadFile.read(filepath);
        //phoneBook = ReadFile.read(filepath2);

        System.out.println("Start searching (quick sort + binary search)...");
        System.out.println(phoneBook.size());
        quickSort(0, phoneBook.size() - 1);

        for (String s : phoneBook) {
            System.out.println(s);
        }

       /* quickSort(0, phoneBook.size());
        for (String s : personsToFind) {
            int indexBin = Collections.binarySearch(phoneBook, s);
            if (indexBin >= 0){
                countBin++;
            }
        }
        System.out.println(countBin);*/


    }

        public void quickSort(int left, int right) {
        if (left < right) {
            int pivotIndex = partition(left, right); // the pivot is already on its place
            quickSort(left, pivotIndex - 1);  // sort the left subarray
            quickSort(pivotIndex + 1, right); // sort the right subarray
        }
    }
    public int partition(int left, int right) {
        String pivot = phoneBook.get(right);  // choose the rightmost element as the pivot
        pivot = (pivot.split(" "))[1];
        int partitionIndex = left; // the first element greater than the pivot

        /* move large values into the right side of the array */
        for (int i = left; i < right; i++) {
            String note = phoneBook.get(i);
            String name = (note.split(" "))[1];
            if (abcOrder(name, pivot)) { // may be used '<' as well
                swap(i, partitionIndex);
                partitionIndex++;
            }
        }

        swap(partitionIndex, right); // put the pivot on a suitable position

        return partitionIndex;
    }

    public void swap(int i, int j) {
        String temp = phoneBook.get(i);
        phoneBook.set(i, phoneBook.get(j));
        phoneBook.set(j, temp);
    }

    public boolean abcOrder(String first, String second) {

        for (int k = 0; k < Math.min(first.length(), second.length()); k++) {

            if (first.toLowerCase().charAt(k) < second.toLowerCase().charAt(k)) {
                return true;
            } else if (first.toLowerCase().charAt(k) > second.toLowerCase().charAt(k)) {
                return false;
            }
        }

        return first.length() <= second.length();

    }

    public void linearSearch() {
        count = 0;
        long startTime = System.currentTimeMillis();
        for (String s : personsToFind) {
            for (String s1 : phoneBook) {
                if (s1.contains(s)) {
                    count++;
                    break;
                }
            }
        }
        elapsedTime = System.currentTimeMillis() - startTime;
    }

    public boolean bubbleSort() {
        long startTime = System.currentTimeMillis();
        for (int i = 0; i < phoneBook.size() - 1; i++) {
            for (int j = 0; j < phoneBook.size() - i - 1; j++) {
                /* if a pair of adjacent elements has the wrong order it swaps them */
                String note = phoneBook.get(j);
                String name = (note.split(" "))[1];
                String note1 = phoneBook.get(j+1);
                String name1 = (note1.split(" "))[1];
                if (name.compareTo(name1) > 0) {
                    String temp = phoneBook.get(j);
                    phoneBook.set(j, phoneBook.get(j+1));
                    phoneBook.set(j + 1, temp);
                }
            }
            elapsedTimeB = System.currentTimeMillis() - startTime;
            if (elapsedTimeB > elapsedTime * 10) {
                return false;
            }
        }
        return true;
    }

    public int jumpSearch(String target) {
        long startTime = System.currentTimeMillis();
        int currentRight = 0; // right border of the current block
        int prevRight = 0; // right border of the previous block

        /* Check the first element */
        if (phoneBook.get(currentRight).equals(target)) {
            return 0;
        }
        /* Calculating the jump length over array elements */
        int jumpLength = (int) Math.sqrt(phoneBook.size());

        /* Finding a block where the element may be present */
        while (currentRight < phoneBook.size() - 1) {

            /* Calculating the right border of the following block */
            currentRight = Math.min(phoneBook.size() - 1, currentRight + jumpLength);
            String note = phoneBook.get(currentRight);
            String name = (note.split(" "))[1];
            String target1 = (target.split(" "))[0];

            if (name.compareTo(target1) >= 0) {
                break; // Found a block that may contain the target element
            }

            prevRight = currentRight; // update the previous right block border
        }
        String note = phoneBook.get(currentRight);
        String name = (note.split(" "))[1];
        String target1 = (target.split(" "))[0];
        /* If the last block is reached and it cannot contain the target value => not found */
        if ((currentRight == phoneBook.size() - 1) && target1.compareTo(name) > 0) {
            return -1;
        }

        /* Doing linear search in the found block */
        int res = backwardSearch(target, prevRight, currentRight);
        elapsedTimeJ = System.currentTimeMillis() - startTime;
        return res;
    }

    public int backwardSearch(String target, int leftExcl, int rightIncl) {
        for (int i = rightIncl; i > leftExcl; i--) {
            String note = phoneBook.get(i);
            String name = (note.split(" "))[1];
            if (note.contains(target)) {

                return i;
            }
        }
        return -1;
    }



}

public class Main {
    public static void main(String[] args) {
        SearchMenu sm = new SearchMenu();
        sm.run();


    }
}
