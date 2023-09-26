import java.util.Scanner;
public class Text01 {

    // 加密函数，将一个正整数按照特定的规则进行加密
    public static int encrypt(int password) {
        // 交换个位和十位
        int ones = password % 10; // 个位数
        int tens = (password / 10) % 10; // 十位数
        password = password - ones * 10 - tens; // 去掉个位和十位
        password = password + ones * 100 + tens; // 交换个位和十位

        // 每位数都加上5
        password = password + 5555;

        // 除以10
        password = password / 10;

        // 乘以2
        password = password * 2;

        // 反转数字
        int reversed = 0; // 用来存储反转后的数字
        while (password > 0) {
            reversed = reversed * 10 + password % 10; // 将最后一位数加到反转后的数字上
            password = password / 10; // 去掉最后一位数
        }
        password = reversed; // 更新密码为反转后的数字

        return password; // 返回加密后的密码
    }

    // 解密函数，将一个正整数按照特定的规则进行解密
    public static int decrypt(int password) {
        // 反转数字
        int reversed = 0; // 用来存储反转后的数字
        while (password > 0) {
            reversed = reversed * 10 + password % 10; // 将最后一位数加到反转后的数字上
            password = password / 10; // 去掉最后一位数
        }
        password = reversed; // 更新密码为反转后的数字

        // 除以2
        password = password / 2;

        // 乘以10
        password = password * 10;

        // 每位数都减去5
        password = password - 5555;

        // 交换个位和十位
        int ones = password % 10; // 个位数
        int tens = (password / 10) % 10; // 十位数
        password = password - ones * 10 - tens; // 去掉个位和十位
        password = password + ones * 100 + tens; // 交换个位和十位

        return password; // 返回解密后的密码
    }

    // 菜单函数，显示系统的功能选项，并返回用户的选择
    public static int menu() {
        System.out.println("欢迎使用密码加密解密系统！");
        System.out.println("请选择您要执行的操作：");
        System.out.println("1. 加密");
        System.out.println("2. 解密");
        System.out.println("3. 退出");
        System.out.print("请输入序号：");
        Scanner input = new Scanner(System.in); // 创建一个扫描器对象，用来接收用户的输入
        int choice = input.nextInt(); // 读取用户输入的整数
        return choice; // 返回用户的选择
    }

    // 主函数，执行系统的主要逻辑
    public static void main(String[] args) {
        int choice = menu(); // 调用菜单函数，获取用户的选择
        while (choice != 3) { // 如果用户没有选择退出，就继续执行
            if (choice == 1) { // 如果用户选择了加密
                System.out.print("请输入一个正整数密码：");
                Scanner input = new Scanner(System.in); // 创建一个扫描器对象，用来接收用户的输入
                int password = input.nextInt(); // 读取用户输入的整数
                if (password > 0) { // 如果密码是正数，就进行加密
                    int encrypted = encrypt(password); // 调用加密函数，获取加密后的密码
                    System.out.println("加密后的密码是：" + encrypted); // 输出加密后的密码
                } else { // 如果密码不是正数，就显示错误信息
                    System.out.println("错误：密码必须是正整数！");
                }
            } else if (choice == 2) { // 如果用户选择了解密
                System.out.print("请输入一个正整数密码：");
                Scanner input = new Scanner(System.in); // 创建一个扫描器对象，用来接收用户的输入
                int password = input.nextInt(); // 读取用户输入的整数
                if (password > 0) { // 如果密码是正数，就进行解密
                    int decrypted = decrypt(password); // 调用解密函数，获取解密后的密码
                    System.out.println("解密后的密码是：" + decrypted); // 输出解密后的密码
                } else { // 如果密码不是正数，就显示错误信息
                    System.out.println("错误：密码必须是正整数！");
                }
            } else { // 如果用户选择了无效的选项，就显示错误信息
                System.out.println("错误：无效的选项！");
            }
            choice = menu(); // 再次调用菜单函数，获取用户的新选择
        }
        System.out.println("感谢您使用密码加密解密系统，再见！"); // 如果用户选择了退出，就显示感谢信息
    }
}