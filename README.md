package com.mycompany.poblacion01;
import java.util.Scanner;
import java.util.Random;
public class Poblacion01 {

    public static void main(String[] args) {
        
        Scanner leer = new Scanner(System.in);
        int[][] matriz1 = new int[8][6];
        int[][] matriz2 = new int[4][2];
        String binario1[] = new String[8];
        Random rand = new Random();
        int num=0, corte=0, temp1, temp2, xr, yr;
        boolean n=true, o=false;
        
        for (int y = 0; y < 8; y++){
            binario1[y] = "";
            for (int x = 0; x < 6; x++){
                matriz1[y][x] = rand.nextInt(2);
                binario1[y] = binario1[y] + matriz1[y][x];
            }
        }
        
        for (int y = 0; y < 4; y++){
            for (int x = 0; x < 2; x++){
                matriz2[y][x] = 0;
            }
        }
        
        System.out.println("--------------Población Inicial--------------");
        for (int y1 = 0; y1 < 8; y1++){
            //Agregar la formula -6x2+3x-6
            temp1 = Integer.parseInt(binario1[y1], 2);
            temp2 = -6 * (temp1*temp1) + (temp1*3) -6;
            System.out.print((y1+1)+") ");
            for (int x1 = 0; x1 < 6; x1++){
                System.out.print(matriz1[y1][x1]);
            }
            System.out.print(" = " + temp2);
            System.out.println("");        
        }
        
        while(n){
            System.out.println("Ingrese un numero mayor que 0 y menor que 6: ");
            if (leer.hasNextInt()) {
                num = leer.nextInt();
                if(num<1 || num>5){
                    System.out.println("El número no está dentro del rango...");
                }else{
                    corte = 6-num;
                    System.out.println("Número de corte: " + num);
                    n=false;
                }
            } else {
                System.out.println("No es un número entero...");
                leer.next();
            }
        }
        
        System.out.println("--------------Parejas de Población--------------");
        for (int y = 0; y < 4; y++) {
            for (int x = 0; x < 2; x++) {
                System.out.println("Ingrese un numero mayor que 0 y menor que 9: ");
                if (leer.hasNextInt()) {
                    num = leer.nextInt();
                    if (num < 1 || num > 8) {
                        System.out.println("El número no está dentro del rango...");
                        x--;
                    } else {
                        for (int y1 = 0; y1 < 4; y1++){
                            for (int x1 = 0; x1 < 2; x1++){
                                if(matriz2[y1][x1]==num){
                                    System.out.println("El número ya existe en la matriz");
                                    o = true;
                                    x--;
                                }else{
                                    o = false;
                                }
                            }
                        } 
                        if(o==false){
                            matriz2[y][x]=num;
                        }
                    }
                } else {
                    System.out.println("No es un número entero...");
                    leer.next();
                    x--;
                }
                for (int y2 = 0; y2 < 4; y2++){
                    System.out.print((y2+1)+") ");
                    for (int x2 = 0; x2 < 2; x2++){
                        System.out.print(matriz2[y2][x2]);
                    }
                    System.out.println("");
                }
            }
        }

        System.out.println("--------------Nueva Población--------------");
        for (int parejay = 0; parejay < 4; parejay++) {
            int pareja1 = matriz2[parejay][0];
            int pareja2 = matriz2[parejay][1];
            for (int x = corte; x < 6; x++) {
                int temp = matriz1[pareja1-1][x];
                matriz1[pareja1-1][x] = matriz1[pareja2-1][x];
                matriz1[pareja2-1][x] = temp;
            }
        }
        
        for (int y = 0; y < 8; y++){
            binario1[y] = "";
            for (int x = 0; x < 6; x++){
                binario1[y] = binario1[y] + matriz1[y][x];
            }
        }
        
        for (int y1 = 0; y1 < 8; y1++) {
            temp1 = Integer.parseInt(binario1[y1], 2);
            temp2 = -6 * (temp1*temp1) + (temp1*3) -6;
            System.out.print((y1 + 1) + ") ");
            for (int x1 = 0; x1 < 6; x1++) {
                System.out.print(matriz1[y1][x1]);
            }
            System.out.print(" = " + temp2);
            System.out.println("");
        }
        
        System.out.println("--------------Mutación--------------");
        xr = rand.nextInt(6);
        yr = rand.nextInt(6);
        System.out.println("---La Mutación se hará en la posición [" + yr + "] [" + xr + "]");
        
        if(matriz1[yr][xr]==0){
            matriz1[yr][xr]=1;
        }else{
            matriz1[yr][xr]=0;
        }
        
        for (int y = 0; y < 8; y++){
            binario1[y] = "";
            for (int x = 0; x < 6; x++){
                binario1[y] = binario1[y] + matriz1[y][x];
            }
        }
        
        for (int y1 = 0; y1 < 8; y1++) {
            temp1 = Integer.parseInt(binario1[y1], 2);
            temp2 = -6 * (temp1*temp1) + (temp1*3) -6;
            System.out.print((y1 + 1) + ") ");
            for (int x1 = 0; x1 < 6; x1++) {
                System.out.print(matriz1[y1][x1]);
            }
            System.out.print(" = " + temp2);
            System.out.println("");
        }
        
       
    }
}
