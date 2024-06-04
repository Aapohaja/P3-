#include <iostream>
#include <string>

//biar bisa gerak kang
class Moveable {
protected:
    int x_position;
    int y_position;
    int hp = 100;

public:
    Moveable(int x, int y) : x_position(x), y_position(y) {}

    int getHp() const {
        return hp;
    }

    void setHp(int newHp) {
        hp = newHp;
    }

    int getXPosition() const {
        return x_position;
    }

    int getYPosition() const {
        return y_position;
    }
};

// buat bisa nyerang kang
class Attackable {
public:
    int attackPower = 10;

    int getAttackPower() const {
        return attackPower;
    }

    void setAttackPower(int power) {
        attackPower = power;
    }

    virtual void attack(Moveable &target) {
        int damage = attackPower;
        target.setHp(target.getHp() - damage);
        std::cout << "kena pukul " << damage << " damage!" << std::endl;
    }
};

// untuk ngdefenf kang
class Defendable {
public:
    int defensePower = 2;

    int getDefensePower() const {
        return defensePower;
    }

    void setDefensePower(int power) {
        defensePower = power;
    }

    void defend(int &damage) {
        damage -= defensePower;
        if (damage < 0) damage = 0;
        std::cout << "Defended with " << defensePower << " power!" << std::endl;
    }
};


class Warrior : public Moveable, public Attackable {
public:
    std::string nama;

    Warrior(std::string name, int x, int y) : Moveable(x, y), nama(name) {}
};


class Mage : public Moveable, public Attackable, public Defendable {
public:
    std::string nama;

    Mage(std::string name, int x, int y) : Moveable(x, y), nama(name) {}
};


class Healer : public Moveable, public Defendable {
public:
    std::string nama;

    Healer(std::string name, int x, int y) : Moveable(x, y), nama(name) {}

    void heal() {
   if (hp < 100) {
            this->hp += 5;
            if (hp > 100) {
                hp = 100;
            }
            std::cout << "nambah 5 HP. Current HP: " << hp << std::endl;
        } else if (hp == 100) {
            std::cout << "udah maks jangan maruk" << std::endl;
        }
    }
};

int main() {
    Warrior budi("Budi", 0, 0);
    Mage jaya("Jaya", 1, 1);
    Healer joko("Joko", 2, 2);

    
    budi.attack(jaya);
    jaya.defend(budi.attackPower);
    jaya.attack(budi);
    jaya.attack(joko);
    joko.heal();//buat buktiin bisa keluar "nambah 5 HP. Current HP: "
    joko.heal();
    joko.heal();//buat buktiin bisa keluar "udah maks jangan maruk"

    return 0;
}
