# Robocode-War-Machine

package competicao;
import robocode.* robocode.control robocode.control.events; 
/**
 * OlaMundo - a robot by (War_Machine)
 */



/*----------------------------------------------------Eventos-De-Movimentação----------------------------------------------------*/
public class OlaMundo extends Robot
{
	public void run() 
	{
		//setColors(Color.red,Color.blue,Color.green); // body,gun,radar
		
		if (colisaoWarnig() == 1) //Chamada da função colisaoWarnig
		{
			back(100);
			turnGunRight(360);
		}
		else
		{
			while(true) 
			{
				ahead(100);
				turnGunRight(360);
				back(100);
				turnGunRight(360);
			}
		}
	}
	
	public int colisaoWarnig() //Função para evitar colisões com as paredes e assim evitar danos
	{
		if (getX() < 50 || getX() > getBattlefieldWidth() - 50 || getY() < 50 || getY() > getBattlefieldHeight() - 50)//Nessa condicional o programa verifica em que dimenção do plano o robo está depois tira de seu tamnho e assim identifica se ele vai colidir ou não
		{
			return 1;
		}
		else
		{
			return 2;
		}
	}
/*----------------------------------------------------Eventos-De-Movimentação----------------------------------------------------*/	  
  

 
/*-----------------------------------------------------Eventos-Dano-Efetuado-----------------------------------------------------*/
	public void onScannedRobot(ScannedRobotEvent e) 
	{
		 turnGunRight(rotacaoOtimizada(e.getBearing()+getHeading-getRadarHeading()));
		 
		 if (e.getEnergy < 12)
		 {
		 	tiroFatal(e.getEnergy);
		 }
		 
		 else
		 {
		 	tiroOtimizado(e.getDistance());
		 }
		  
	}
	
	public double rotacaoOtimizada(Angulo)
	{
		if (Angulo > -180 && Angulo <= 180)
		{
			return Angulo;
		}
		
		double Bestang;
		Bestang = Angulo;
		
		while (Bestang<=-180)
		{
			Bestang = 360 + Bestang;
		}
		
		while (Angulo > 180)
		{
			Bestang = 360 - Bestang;
		}
		
		return Bestang;
	} 
	
	public void tiroOtimizado(double Distancia)
	{
		if (Distancia > 100)
		{
			fire(1);
		}
		else if (Distancia < 100 && Distancia > 50)
		{
			fire(2);
		}
		else if (Distancia < 50)
		{
			fire(3);
		}
	}
	
	public void tiroFatal(double energia)
	{
		double Tiro;
		
		Tiro = (energia/4) + 0.1; /*Bruno vê o que fica melhor onde esta o 0.1(1, ou 0.85 ou 0.15 ou 0.1)*/
		fire(Tiro);
	}
/*-----------------------------------------------------Eventos-Dano-Efetuado-----------------------------------------------------*/



/*-----------------------------------------------------Eventos-Dano-Sofrido------------------------------------------------------*/
	public void onHitByBullet(HitByBulletEvent e) 
	{
		back(10);
	}
/*-----------------------------------------------------Eventos-Dano-Sofrido------------------------------------------------------*/



/*-------------------------------------------------------------------------------------------------------------------------------*/
	public void onHitWall(HitWallEvent e) 
	{
		back(20);
	}
/*-------------------------------------------------------------------------------------------------------------------------------*/	
}
