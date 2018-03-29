//3�� ��������
/*
Ŭ������ �ٸ� Ŭ������ �ּ����� �������� �������� �ϴ°� >> �и������� �ڵ带 �����. >> �ʹ� ������ ���踦 ������ �Ǹ� �������� ����.
*/
//ex. �������� ���� �ڵ�
var Westeros;
(function (Westeros) {
	var Ruler = (function(){
		function Ruler(){
		this.house = new Westeros.Houses.Targaryen();
		}
		return Ruler;
	})();	//Westeros ���� ����, Ruler�� �������ڸ��� ������ Targaryen���� ���� ����� > ���� ����
	Westeros.Ruler = Ruler;
})(Westeros || (Westeros = {}));


//1. �߻� ���丮 ����
/*��ü�� ��ü���� ������ �� ä ��ä�� �����ϴ� ���.
  ������ �ۼ��ߴ� �ҽ����� ������ ���ø����̼� ���� ����.
  **����� �������̽��� ��ü Ŭ����(Concrete factory)���� ������ return��.
*/

/*cf. ��Ÿ����(Duck Typing)
  ���� Ÿ������ �� ������, ��ü�� ���� �� �޼ҵ��� ������ ��ü�� Ÿ���� �����ϴ� ���� ����.(>�̸� ��ü�� Ÿ���� �����Ǿ� ���� ����)
  ��Ÿ������ ��ü�� � Ÿ�Կ� �ɸ��� ������ �޼ҵ带 ���ϸ� �ش� Ÿ������ ���ϴ� ������ ������.
  �������(Ư���� ��ǥ�� ���� �ʿ��� �ð�,���ҽ�,�ڿ���)�� ���� �� ������ ��Ȯ�Ǽ��� ���� �� ����.
*/

/* cf. ��ⱸ��
*/

//1)����
//��ü�� concrete class ����
var KingJoffery = (function() {
	function KingJoffery() {
		console.log("I'm Joffery");
	}
	KingJoffery.prototype.makeDecision = function() {
		console.log("Joffery makes decision");
	};
	KingJoffery.prototype.marry = function() {
		console.log("Joffery married with Sansa");
	};
	return KingJoffery;
})();

var LordTywin = (function () {
	function LordTywin() {
		console.log("I'm Tywin");
	};
	LordTywin.prototype.makeDecision = function(){
		console.log("lani's always pay his depbts");
	};
	return LordTywin
})();	
//��ü���� factory ����
var LannisterFactory = (function() {
	function LannisterFactory(){
	};
	LannisterFactory.prototype.getKing = function(){
		return new KingJoffery();
	};
	LannisterFactory.prototype.getHand = function(){
		return new LordTywin();
	};
	return LannisterFactory;
})();
//���丮 ����� ���� Ŭ����
var CourtSession = (function(){
	function CourtSession(abstractFactory) {
		this.abstractFactory = abstractFactory;	//�Ķ���� ������ ���丮 ���� 
		this.COMPLAINT_THRESHOLD = 10;
	}
	CourtSession.prototype.complaintPresented = function(complaint)
	{
		if(complaint.severity < this.COMPLAINT_THRESHOLD){
			this.abstractFactory.getHand().makeDecision();
		}else
			this.abstractFactory.getKing().makeDecision();
	};	//�Ķ���� ���� ���� �б�
	return CourtSession;
})();

//2. ���� ����
/*Ŭ������ ������ ��Ŀ� ���� �������̽� ������ �޶����� ���... Ŭ���� ���� �ܼ�ȭ&���� ���ľ��� Ŭ���� ������ �� ���.
  �����ڰ� Ŭ���� ������ ������ �ʵ���. ������ �߰� ���� ���� ����� ����. > ��ü �����ϴµ� �ʿ��� ������ �߾�����ȭ �Ͽ� 
  ex.��ʸ�Ʈ..  ��ƿ��Ƽ Ŭ���� ����
*/
//����
//1) ��ƿ��Ƽ Ŭ���� ��� ( �߾� ������ �ҷ��� Ŭ�������� ���� )
var Event = (function () {
	function Event(name){
		this.name = name;
	}
	return Event;
})();
var Prize = (function() {
	function Prize(name){
		this.name = name;
	}
	return Prize;
})();

var Attendee = (function() {
	function Attendee(name){
		this.name = name;
	}
	return Attendee;
})();
Westeros.Event = Event;
Westeros.Prize = Prize;
Westeros.Attendee = Attendee;

var Tournament = (function(){
	this.Events = [];
	function Tournament(){
	}
	return Tournament;
})();
Westeros.Tournament = Tournament;

//���δٸ� ��ʸ�Ʈ�� �����ϴ� ���� ���� > 
var LannisterTournamentBuilder = (function() {
	function LannisterTournamentBuilder(){
	}
	LannisterTournamentBuilder.prototype.build = function(){
		var tournament = new Tournament();
		tournament.events.push(new Event("Joust"));
		tournament.events.push(new Event("Melee"));

		tournament.attendees.push(new Attendee("Jamie"));

		tournament.prizes.push(new Prize("gold"));
		tournament.prizes.push(new Prize("More gold"));

		return tournament;
	};
	return LannisterTournamentBuilder;
})();
Westeros.LannisterTournamentBuilder = LannisterTournamentBuilder;

//������ ���ڷ� �޾� �����ϴ� ����. > ����
var TournamentBuilder = (function(){
	function TournamentBuilder(){
	}
	TournamentBuilder.prototype.build = function(builder){
		return builder.build();
	}
	return TournamentBuilder;
})();

/*å ���̾�׷� ����..
  Director : TournamentBuilder
  Builder : LannisterTournamentBuilder
			BaratheonTournamentBuilder
  ����ڰ� Director�� ���� ���� �����ϴ°ɷ� �����ߴµ�... ��¡...??
*/

//3.���丮 �޼ҵ� ����
/*�߻����丮 : ���ü��� ���� Ŭ�������� ������ ����
  �������� : ���հ�ü�� ����
  ���丮 �޼ҵ� : �������̽��� ��� ���������� ���� ���� ���� Ŭ������ �������̽��� ���ο� �ν��Ͻ��� ��û�� �� �ֵ��� �����.
*/

// ����
var WaterGod = (function() {
	function WaterGod(){
	}
	WaterGod.prototype.prayTo = function(){
		console.log("To WaterGod")
	};
	return WaterGod;
})();
var AncientGod = (function(){
	function AncientGod(){
	}
	AncientGod.prototype.prayTo = function(){
		console.log("To AncientGod")
	}
	return AncientGod;
})();
var DefaultGod = (function(){
	function DefaultGod(){
	}
	DefaultGod.prototype.prayTo = function(){
		console.log("To DefaultGod")
	}
	return DefaultGod;
})();
Religion.WaterGod = WaterGod;
Religion.AncientGod = AncientGod;
Religion.DefaultGod = DefaultGod;

//���丮 �ʿ� > �б�
var GodFactory = (function() {
	function GodFactory(){
	};
	GodFactory.Build = function(godName){
		if(godName ==="water")
			return new WaterGod();
		if(godName ==="ancient")
			return new AncientGod();
		return new DefaultGod();
	}
	return GodFactory;
})();

var GodDeterminant = (function(){
	function GodDeterminant(religionName, prayerPurpose){
		this.religionName = religionName;
		this.prayerPurpose = prayerPurpose;
	}
	return GodDeterminant;
})();

var Prayer = (function() {
	function Prayer(){
	}
	Prayer.prototype.pray = function (godName) {
		GodFactory.Build(godName).prayTo();
	}
	return Prayer;
})();

//����ü (�̱���)
/*���� ���� ���̴� ������ �ϳ�.
  �ֱ� ��Ⱓ ��ȣ�� ������. 
  ����> 1.��������..
*/
//����
var Westeros;
(function (Westeros) {
	var Wall = (function() {
		console.log("Wall")
		function Wall(){
			this.height = 0;
			if(Wall._instance)
				return Wall._instance;
			Wall._instance = this;
	}
	Wall.prototype.setHeight = function(height){
				console.log("setHeight")
		this.height = height
	};
	Wall.prototype.getStatus = function(){
				console.log("getStatus")
		console.log("Wall is " + this.height + " meter tall");
	};
	Wall.getInstance = function(){
				console.log("getInstance")
		if(!Wall._instance){
			Wall._instance = new Wall();
		}
		return Wall._instance;
	};
	Wall._instance = null;
	return Wall;
})();
Westeros.Wall = Wall;
})(Westeros || (Westeros = {}));

//���� : �������� ��� ��ȭ, ���� �׽�Ʈ�� �׽�Ʈ�ϱ� �����, ����ü�� �ʹ� ���� ������ ����(���� å���� ��Ģ ����)

//5)������Ÿ�� > js����� �����ϴµ� ���Ǵ� ��Ŀ����
/*���� ��ü�� ����

*/
//����
//������ ��ü�� ������ ���ο� ��ü�� ����
function clone(source, destination) {
	for(var attr in source.prototype){
		destination.prototype[attr] = source.prototype[attr];
	}
}
//�ڽ��� ���纻�� ��ȯ�ϴµ� ����� �� �ֵ��� ����
var Westeros;
	(function (Westeros){
		(function (Families){
			var Lannister = (function () {
				function Lannister(){
				}
				Lannister.prototype.clone = function(){
					var clone = new Lannister();
					for (var attr in this){
						clone[attr] = this[attr];
					}
					return clone;
				};
				return Lannister;
			})();
			Families.Lannister = Lannister;
		})(Westeros.Families||Westeros.Families = {}));
		var Families = Westeros.Families;
	})(Westeros || Westeros = {}));