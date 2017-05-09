# test
#日历
package com.dingli.test;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;
import java.util.GregorianCalendar;
import java.util.Scanner;

public class Demo4 {
	private static Scanner sc = new Scanner(System.in);

	public static void main(String[] args) throws ParseException {
		// TODO Auto-generated method stub
		System.out.println("请输入年-月（yyyy-MM的格式）");
		String str = sc.nextLine();
		showCalendar(str);
	}

	public static void showCalendar(String str) {
		System.out.println("星期日" + "\t星期一" + "\t星期二" + "\t星期三" + "\t星期四" + "\t星期五" + "\t星期六");
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM");
		try {
			// 将字符串转换成日期格式
			Date date = sdf.parse(str);
			Calendar c = new GregorianCalendar();
			// 将日期转换成日里格式
			c.setTime(date);
			// 获取当前月中的某一天
			int day = c.get(Calendar.DAY_OF_WEEK);
			// 获取当前月份
			int month = c.get(Calendar.MONTH) + 1;
			// 获取当前年份
			int year = c.get(Calendar.YEAR);
			// 获取当前月份的天数
			int days = getDays(year, month);
			// 创建数组保存日期(最多36)
			String[] array = new String[36];
			// 数组初始化，全部置空
			for (int i = 0; i < array.length; i++) {
				array[i] = " ";
			}
			// 将当前月的每一天对应添加到数组中
			for (int i = 1; i <= days; i++) {
				array[i + day - 2] = i + "";
			}
			int count = 0;
			// 输出日历
			for (int j = 0; j < array.length; j++) {
				System.out.print(array[j] + "\t");
				count++;
				if (count % 7 == 0) {
					System.out.println();
				}
			}

		} catch (ParseException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

	// 根据年份和月份获取某月的天数
	public static int getDays(int year, int month) {
		int days = 0;
		switch (month) {
		case 1:
		case 3:
		case 5:
		case 7:
		case 8:
		case 10:
		case 12: {
			days = 31;
			break;
		}
		case 4:
		case 6:
		case 9:
		case 11: {
			days = 30;
			break;
		}
		case 2: {
			if (year % 400 == 0 || (year % 4 == 0 && year % 100 != 0)) {
				days = 28;
			} else {
				days = 29;
			}
		}
		}
		return days;
	}
}
