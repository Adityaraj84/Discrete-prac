## practical 1
class SET:
    def __init__(self, elements=None):
        if elements is None:
            elements = []
        self.set = set(elements)

    def ismember(self, element):
        return element in self.set

    def powerset(self):
        from itertools import chain, combinations
        s = list(self.set)
        return list(chain.from_iterable(combinations(s, r) for r in range(len(s)+1)))

    def is_subset(self, other_set):
        return self.set.issubset(other_set.set)

    def union(self, other_set):
        return self.set.union(other_set.set)

    def intersection(self, other_set):
        return self.set.intersection(other_set.set)

    def complement(self, universal_set):
        return universal_set.set.difference(self.set)

    def set_difference(self, other_set):
        return self.set.difference(other_set.set)

    def symmetric_difference(self, other_set):
        return self.set.symmetric_difference(other_set.set)

    def cartesian_product(self, other_set):
        return {(a, b) for a in self.set for b in other_set.set}


def main():
    print("Enter elements of Set A separated by space:")
    set_a = SET(input().split())

    print("Enter elements of Set B separated by space:")
    set_b = SET(input().split())

    print("Enter elements of Universal Set separated by space:")
    universal = SET(input().split())

    while True:
        print("\nMenu:")
        print("1. Check if element is member of Set A")
        print("2. Power set of Set A")
        print("3. Check if Set A is subset of Set B")
        print("4. Union of Set A and Set B")
        print("5. Intersection of Set A and Set B")
        print("6. Complement of Set A")
        print("7. Set Difference (A - B)")
        print("8. Symmetric Difference of Set A and Set B")
        print("9. Cartesian Product of Set A and Set B")
        print("10. Exit")

        choice = int(input("Enter your choice: "))

        if choice == 1:
            elem = input("Enter element to check: ")
            print("Member" if set_a.ismember(elem) else "Not a member")
        elif choice == 2:
            ps = set_a.powerset()
            print("Power Set:")
            for subset in ps:
                print(set(subset))
        elif choice == 3:
            print("Set A is subset of Set B" if set_a.is_subset(set_b) else "Set A is NOT subset of Set B")
        elif choice == 4:
            print("Union:", set_a.union(set_b))
        elif choice == 5:
            print("Intersection:", set_a.intersection(set_b))
        elif choice == 6:
            print("Complement of A:", set_a.complement(universal))
        elif choice == 7:
            print("A - B:", set_a.set_difference(set_b))
        elif choice == 8:
            print("Symmetric Difference:", set_a.symmetric_difference(set_b))
        elif choice == 9:
            print("Cartesian Product:")
            for pair in set_a.cartesian_product(set_b):
                print(pair)
        elif choice == 10:
            print("Exiting...")
            break
        else:
            print("Invalid choice!")


if __name__ == "__main__":
    main()
## practical 2
class RELATION:
    def __init__(self, elements, matrix):
        self.elements = elements  # List of elements (domain)
        self.matrix = matrix      # Adjacency matrix representing the relation
        self.n = len(elements)

    def is_reflexive(self):
        for i in range(self.n):
            if self.matrix[i][i] != 1:
                return False
        return True

    def is_symmetric(self):
        for i in range(self.n):
            for j in range(self.n):
                if self.matrix[i][j] != self.matrix[j][i]:
                    return False
        return True

    def is_anti_symmetric(self):
        for i in range(self.n):
            for j in range(self.n):
                if i != j and self.matrix[i][j] == 1 and self.matrix[j][i] == 1:
                    return False
        return True

    def is_transitive(self):
        for i in range(self.n):
            for j in range(self.n):
                if self.matrix[i][j]:
                    for k in range(self.n):
                        if self.matrix[j][k] and not self.matrix[i][k]:
                            return False
        return True

    def relation_type(self):
        r = self.is_reflexive()
        s = self.is_symmetric()
        a = self.is_anti_symmetric()
        t = self.is_transitive()

        print(f"Reflexive: {r}")
        print(f"Symmetric: {s}")
        print(f"Anti-Symmetric: {a}")
        print(f"Transitive: {t}")

        if r and s and t:
            return "Equivalence Relation"
        elif r and a and t:
            return "Partial Order Relation"
        else:
            return "None"
## Practical 5
def evaluate_polynomial(coeffs, n):
    result = 0
    degree = len(coeffs) - 1
    for i in range(len(coeffs)):
        result += coeffs[i] * (n ** (degree - i))
    return result

def main():
    # Example: f(n) = 4n^2 + 2n + 9
    # Coefficients: [4, 2, 9]  => 4n^2 + 2n + 9
    coeffs = list(map(int, input("Enter coefficients of the polynomial (highest degree first): ").split()))
    n = int(input("Enter the value of n: "))
    
    value = evaluate_polynomial(coeffs, n)
    print(f"Value of the polynomial at n = {n} is: {value}")

if __name__ == "__main__":
    main()
# practical 6
def is_complete_graph(adj_matrix):
    n = len(adj_matrix)
    for i in range(n):
        for j in range(n):
            if i == j:
                if adj_matrix[i][j] != 0:
                    return False
            else:
                if adj_matrix[i][j] != 1:
                    return False
    return True

def main():
    n = int(input("Enter number of vertices in the graph: "))
    print("Enter the adjacency matrix row by row (space separated 0s and 1s):")

    adj_matrix = []
    for i in range(n):
        row = list(map(int, input(f"Row {i+1}: ").split()))
        if len(row) != n:
            print("Invalid row length! Must be equal to number of vertices.")
            return
        adj_matrix.append(row)

    if is_complete_graph(adj_matrix):
        print("The graph is a Complete Graph.")
    else:
        print("The graph is NOT a Complete Graph.")

if __name__ == "__main__":
    main()
## 3
from itertools import permutations, product

def get_input_digits():
    digits = input("Enter digits separated by space: ").split()
    length = int(input("Enter length of each permutation: "))
    return digits, length

def generate_without_repetition(digits, length):
    return list(permutations(digits, length))

def generate_with_repetition(digits, length):
    return list(product(digits, repeat=length))

def main():
    digits, ut("Enter choice (1 or 2): "))

    if choice == 1:
        perms = generate_without_repetition(digits, length)
    elif choice == 2:
        perms = generate_with_repetition(digits, length)
    else:
        print("Invalid choice!")
        return

    print("\nGenerated Permutations:")
    for p in perms:
        print(''.join(p))

if __name__ == "__main__":
    main()
## practical 4
from itertools import product

def find_solutions(n, C):
    print(f"Solutions to x1 + x2 + ... + x{n} = {C} where xi ≥ 0:")

    count = 0
    # Generate all combinations of n numbers from 0 to C (brute force)
    for combo in product(range(C + 1), repeat=n):
        if sum(combo) == C:
            print(combo)
            count += 1

    print(f"\nTotal solutions: {count}")

def main():
    n = int(input("Enter number of variables (n): "))
    C = int(input("Enter the constant value (C ≤ 10): "))

    if C > 10 or n <= 0:
        print("Invalid input! Ensure C ≤ 10 and n > 0.")
        return

    find_solutions(n, C)

if __name__ == "__main__":
    main()
