#include <iostream>
#include <vector>
#include <chrono>
#include <algorithm>

using namespace std;
using namespace chrono;

void sequential_search(const vector<int>& arr, int target) {
    int n = arr.size();
    int comparisons = 0;
    for (int i = 0; i < n; ++i) {
        comparisons++;
        if (arr[i] == target) {
            cout << "Sequential Search found " << target << " at position " << i << " with " << comparisons << " comparisons." << "\n";
            return;
        }
    }
    cout << "Sequential Search did not find " << target << " in the array.\n";
}

void binary_search(const vector<int>& arr, int target) {
    int low = 0, high = arr.size() - 1;
    int comparisons = 0;
    while (low <= high) {
        comparisons += 2; // Assuming 1 comparison for each binary step (ignoring the loop condition)
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) {
            cout << "Binary Search found " << target << " at position " << mid << " with " << comparisons << " comparisons.\n";
            return;
        }
        if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    cout << "Binary Search did not find " << target << " in the array.\n";
}

int main() {
    vector<int> data_items;
    int n;
    int target;
    auto start_time = high_resolution_clock::now();
    
    // Sequential Search
    sequential_search(data_items, target);
    auto sequential_end_time = high_resolution_clock::now();
    auto sequential_duration = duration_cast<microseconds>(sequential_end_time - start_time);
    cout << "Sequential Search took " << sequential_duration.count() << " microseconds.\n";

    // Binary Search
    start_time = high_resolution_clock::now();
    binary_search(data_items, target);
    auto binary_end_time = high_resolution_clock::now();
    auto binary_duration = duration_cast<microseconds>(binary_end_time - start_time);
    cout << "Binary Search took " << binary_duration.count() << " microseconds.\n";

    int num_comparisons_sequential = 0, num_comparisons_binary = 0;
    if (sequential_search(data_items, target) != "Sequential Search did not find") {
        num_comparisons_sequential = comparisons;
    }
    if (binary_search(data_items, target) != "Binary Search did not find") {
        num_comparisons_binary = comparisons;
    }

    if (num_comparisons_sequential < num_comparisons_binary) {
        cout << "Sequential Search is more efficient.\n";
    } else {
        cout << "Binary Search is more efficient.\n";
    }

    return 0;
}
