package com.tax;

import java.io.BufferedReader;
import java.io.InputStreamReader;

public class TaxCalc {	
	double taxslab[][] = new double[4][7];
	
	public void setTaxslab() {
		//Single filing slab
		taxslab[0][0] = 0; //slab for 10%
		taxslab[0][1] = 9276; //slab for 15%
		taxslab[0][2] = 37651; //slab for 25%
		taxslab[0][3] = 91151; //slab for 28%
		taxslab[0][4] = 190151; //slab for 33%
		taxslab[0][5] = 413351; //slab for 35%
		taxslab[0][6] = 415051; //slab for 36.6%
		
		//Married Filing Joint
		taxslab[1][0] = 0; //slab for 10%
		taxslab[1][1] = 18551; //slab for 15%
		taxslab[1][2] = 75301; //slab for 25%
		taxslab[1][3] = 151901; //slab for 28%
		taxslab[1][4] = 231451; //slab for 33%
		taxslab[1][5] = 413351; //slab for 35%
		taxslab[1][6] = 466951; //slab for 36.6%
		
		//Married Filing Seperately
		taxslab[2][0] = 0; //slab for 10%
		taxslab[2][1] = 9276; //slab for 15%
		taxslab[2][2] = 37651; //slab for 25%
		taxslab[2][3] = 75951; //slab for 28%
		taxslab[2][4] = 115726; //slab for 33%
		taxslab[2][5] = 206676; //slab for 35%
		taxslab[2][6] = 233476; //slab for 36.6%

		//Head Of household
		taxslab[3][0] = 0; //slab for 10%
		taxslab[3][1] = 13251; //slab for 15%
		taxslab[3][2] = 50401; //slab for 25%
		taxslab[3][3] = 130151; //slab for 28%
		taxslab[3][4] = 210801; //slab for 33%
		taxslab[3][5] = 413351; //slab for 35%
		taxslab[3][6] = 441001; //slab for 36.6%
	}
	
	public double calc(int index, double taxinc) {
		double temp=taxinc, tax=0, t=0, t1=0;
		
		if(taxinc != 0) {			
			t = taxslab[index][1] - taxslab[index][0];
			t1 = temp > t ? t : temp;
			
			tax = tax + 0.10 * t1;
			temp=temp - t1;
			System.out.println("10% Slab : Temp = " + temp + " : tax="+tax);		
		}
		
		if(taxinc > taxslab[index][1]) {
			t = taxslab[index][2] - taxslab[index][1];
			t1 = temp > t ? t : temp;
			
			tax = tax + 0.15 * t1;
			temp=temp - t1;
			System.out.println("15% Slab : Temp = " + temp + " : tax="+tax);			
		}
		
		if(taxinc > taxslab[index][2]) {
			t = taxslab[index][3] - taxslab[index][2];
			t1 = temp > t ? t : temp;
			
			tax = tax + 0.25 * t1;
			temp=temp - t1;
			System.out.println("25% Slab : Temp = " + temp + " : tax="+tax);	 
		}
		
		if(taxinc > taxslab[index][3]) {
			t = taxslab[index][4] - taxslab[index][3];
			t1 = t > temp ? t : temp;
			
			tax = tax + 0.28 * t1;
			temp=temp - t1;
			System.out.println("28% Slab : Temp = " + temp + " : tax="+tax);	 
		}
		
		if(taxinc > taxslab[index][4]) {
			t = taxslab[index][5] - taxslab[index][4];
			t1 = t > temp ? t : temp;
			
			tax = tax + 0.33 * t1;
			temp=temp - t1;	
			System.out.println("33% Slab : Temp = " + temp + " : tax="+tax); 
		}
		
		if(taxinc > taxslab[index][5]) {
			t = taxslab[index][6] - taxslab[index][5];
			t1 = t > temp ? t : temp;
			
			tax = tax + 0.35 * t1;
			temp=temp - t1;	 
			System.out.println("35% Slab : Temp = " + temp + " : tax="+tax);
		}
		
		if(taxinc > taxslab[index][6]) {			
			tax = tax + 0.396 * temp;

			System.out.println("39.6% Slab : Temp = " + temp + " : tax="+tax);
		}		
		return tax;
	}
	
	public double calcTax(int fs, double taxinc) {
		double returnval=0;
		switch(fs){
			case 0: returnval = calc(fs, taxinc);
				break;
			case 1: returnval = calc(fs, taxinc);
				break;
			case 2: returnval = calc(fs, taxinc);
				break;
			case 3: returnval = calc(fs, taxinc);
				break;
			default: System.out.println("Invalid Filing status!!!");
				returnval=-1;
				break;
		}
		
		return returnval;
	}

	public static void main(String[] args) {
		double taxableIncome=0, tax=0;
		int filingStatus=-1;
		BufferedReader br;
		TaxCalc tc=new TaxCalc();
		
		tc.setTaxslab();
		
		System.out.println("Welcome to Personal Tax Calculator !!!");
		
		try {
			System.out.print("Enter filing status : ");
			br=new BufferedReader(new InputStreamReader(System.in));
			filingStatus = Integer.parseInt(br.readLine());
			
			System.out.print("Enter taxable Income: ");
			br=new BufferedReader(new InputStreamReader(System.in));
			taxableIncome= Integer.parseInt(br.readLine());
			
			System.out.println("Filing Status = " + filingStatus + " : Taxable Income = " + taxableIncome);
			
			tax= tc.calcTax(filingStatus, taxableIncome);
			
			if(tax<0) {
				System.out.println("Please try again. Thank you!!!");
			}
			else {
				System.out.println("Tax is " + tax);
			}			
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
# TaxCalculater
Basic program of Tax Calculation
