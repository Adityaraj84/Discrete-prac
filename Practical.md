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


def input_relation():
    n = int(input("Enter number of elements in the set: "))
    elements = input("Enter the elements separated by space: ").split()

    print("Enter the adjacency matrix (rows separated by newlines, 0/1 only):")
    matrix = []
    for _ in range(n):
        row = list(map(int, input().split()))
        matrix.append(row)

    return RELATION(elements, matrix)


def main():
    relation = input_relation()
    result = relation.relation_type()
    print("This relation is:", result)


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
    digits, length = get_input_digits()
    
    print("\nChoose permutation type:")
    print("1. Without Repetition")
    print("2. With Repetition")
    choice = int(input("Enter choice (1 or 2): "))

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
