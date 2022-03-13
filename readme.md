Ce back-end fournit une API et un backoffice pour les lecteurs d'epubs en ligne, et a été réalisé sous Symfony 5.4 pour un projet de fin d'étude.

Marche à suivre pour avoir le backend chez vous, fonctionnel, avec tout ce qu'il y a sur la base de données du serveur et ses fichiers epubs et compagnie !

Tout simplement : Clonez ce repo, après ouvrez VSCode dans le dossier BookOWonder, créez un fichier .env.local avec ceci dedans :

DATABASE_URL="mysql://NOMUTILISATEUR:MOTDEPASSE@127.0.0.1:3306/bookowonder?serverVersion=mariadb-VERSIONDEMARIADB"

APP_ENV=prod



On ouvre un terminal dans le dossier BookOWonder et on fait un "composer install --no-dev" puis un "php -S 0.0.0.0:8080 -t public"


Maintenant faites un "php bin/console d:d:c" , qui aura pour effet de créer la base de données puis allez sur Adminer, sur la base de donnée bookowonder et cliquez sur SQL command puis copiez collez tout ce qui suit, et voilà tout est bon  ♥

Poue se connecter au backoffice : login admin, mot de passe adminadminadmin


SET NAMES utf8;
SET time_zone = '+00:00';
SET foreign_key_checks = 0;
SET sql_mode = 'NO_AUTO_VALUE_ON_ZERO';

SET NAMES utf8mb4;

DROP TABLE IF EXISTS `audio`;
CREATE TABLE `audio` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `music` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `image` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  `updated_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `audio` (`id`, `name`, `music`, `image`, `created_at`, `updated_at`) VALUES
(4,	'Lofi (détente et chill)',	'https://www.youtube.com/watch?v=5qap5aO4i9A',	'61bd9bba4adb2.jpg',	'2021-12-18 08:28:41',	'2021-12-18 12:09:07'),
(5,	'Horreur',	'https://www.youtube.com/watch?v=U-xs6SbOcjY&t',	'61bd9bf3e2a14.jpg',	'2021-12-18 08:29:39',	'2021-12-18 12:08:45'),
(6,	'Science-fiction',	'https://www.youtube.com/watch?v=9kEMzXw7P2A',	'61bd9c59ddecc.jpg',	'2021-12-18 08:31:21',	NULL),
(7,	'Fantasy',	'https://www.youtube.com/watch?v=j1BO2Y8RI7A',	'61bd9c9ec055f.jpg',	'2021-12-18 08:32:30',	NULL),
(8,	'Désert',	'https://www.youtube.com/watch?v=4E-_Xpj0Mgo',	'61bd9ce7aa49e.jpg',	'2021-12-18 08:33:43',	'2021-12-18 12:10:21'),
(9,	'Pluie',	'https://www.youtube.com/watch?v=y4h_4NIOxuY',	'61bd9d380c6e6.jpg',	'2021-12-18 08:35:04',	'2021-12-18 12:09:29'),
(10,	'Vent',	'https://www.youtube.com/watch?v=vp2TXUVMNm8',	'61bd9d87d0d65.jpg',	'2021-12-18 08:36:23',	'2021-12-18 12:09:35'),
(11,	'Neige',	'https://www.youtube.com/watch?v=hZYSMkLSolc',	'61bd9de090e2d.jpg',	'2021-12-18 08:37:52',	'2021-12-18 12:09:42'),
(12,	'Thriller',	'https://www.youtube.com/watch?v=EcLZE4KVc_E',	'61bd9ee53357a.jpg',	'2021-12-18 08:42:13',	'2021-12-18 08:42:17');

DROP TABLE IF EXISTS `audio_category`;
CREATE TABLE `audio_category` (
  `audio_id` int(11) NOT NULL,
  `category_id` int(11) NOT NULL,
  PRIMARY KEY (`audio_id`,`category_id`),
  KEY `IDX_891630373A3123C7` (`audio_id`),
  KEY `IDX_8916303712469DE2` (`category_id`),
  CONSTRAINT `FK_8916303712469DE2` FOREIGN KEY (`category_id`) REFERENCES `category` (`id`) ON DELETE CASCADE,
  CONSTRAINT `FK_891630373A3123C7` FOREIGN KEY (`audio_id`) REFERENCES `audio` (`id`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `audio_category` (`audio_id`, `category_id`) VALUES
(4,	2),
(5,	1),
(6,	4),
(7,	2),
(8,	2),
(8,	4),
(9,	3),
(9,	4),
(10,	2),
(10,	3),
(10,	4),
(11,	2),
(11,	3),
(12,	5);

DROP TABLE IF EXISTS `author`;
CREATE TABLE `author` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `firstname` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `lastname` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  `updated_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `author` (`id`, `firstname`, `lastname`, `created_at`, `updated_at`) VALUES
(1,	'Frank',	'Herbert',	'2021-12-07 10:56:34',	NULL),
(2,	'Amélie',	'Nothomb',	'2021-12-07 10:56:41',	NULL),
(3,	'Alex',	'Vede',	'2021-12-07 10:56:53',	NULL),
(4,	'Philip ',	'Pullman',	'2021-12-07 10:57:31',	NULL),
(5,	'Lewis',	'Caroll',	'2021-12-09 12:58:31',	NULL),
(6,	'Pierre',	'Lotti',	'2021-12-18 09:22:47',	NULL),
(7,	'Alphonse',	'Daudet',	'2021-12-18 09:23:22',	NULL),
(8,	'Joséphine',	'Dandurand',	'2021-12-18 09:23:52',	NULL),
(9,	'Jennifer',	'Armentrout',	'2021-12-18 09:25:48',	NULL),
(10,	'Grégory',	'Covin',	'2021-12-18 09:27:01',	NULL),
(11,	'Pierre',	'Bordage',	'2021-12-18 09:27:49',	NULL),
(12,	'Lincoln Child',	'Douglas Preston',	'2021-12-18 09:29:58',	NULL),
(13,	'John',	'Polidori',	'2021-12-18 09:31:09',	NULL),
(14,	'Isabelle',	'Haury',	'2021-12-18 09:31:54',	NULL),
(16,	'Jeanne',	'Stephens',	'2021-12-18 10:18:09',	NULL),
(17,	'Robin',	'Elliott',	'2021-12-18 10:18:19',	NULL),
(18,	'Jan',	'Mathews',	'2021-12-18 10:18:39',	NULL),
(19,	'Meg',	'Dominique',	'2021-12-18 10:33:09',	NULL);

DROP TABLE IF EXISTS `book`;
CREATE TABLE `book` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `author_id` int(11) DEFAULT NULL,
  `editor_id` int(11) DEFAULT NULL,
  `title` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `synopsis` longtext COLLATE utf8mb4_unicode_ci NOT NULL,
  `picture` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `epub` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `isbn` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `published_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  `updated_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  `is_home` tinyint(1) NOT NULL,
  `front_pic` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `IDX_CBE5A331F675F31B` (`author_id`),
  KEY `IDX_CBE5A3316995AC4C` (`editor_id`),
  CONSTRAINT `FK_CBE5A3316995AC4C` FOREIGN KEY (`editor_id`) REFERENCES `editor` (`id`),
  CONSTRAINT `FK_CBE5A331F675F31B` FOREIGN KEY (`author_id`) REFERENCES `author` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `book` (`id`, `author_id`, `editor_id`, `title`, `synopsis`, `picture`, `epub`, `isbn`, `published_at`, `created_at`, `updated_at`, `is_home`, `front_pic`) VALUES
(2,	3,	2,	'A la croisée des mondes : les royaumes du Nord',	'Élevée dans le très austère Jordan College à Oxford, Lyra Belacqua accompagnée de son dæmon Pantalaimon, apprend accidentellement l\'existence de la Poussière, une étrange particule élémentaire que le Magisterium (l\'organe exécutif de l\'Église) pense être la conséquence du Péché originel. L’Église a en effet observé que cette Poussière est moins attirée par l\'innocence des enfants que par l\'expérience des adultes. Des savants, avec la bénédiction de l’Église, poursuivent d\'horribles expériences sur la Poussière en utilisant des enfants kidnappés dans toute l\'Angleterre et envoyés dans les royaumes glacés du Grand Nord.',	'61bdb11f687dc.jpg',	'61bde36e61e6c.epub',	NULL,	'1995-10-03 10:02:00',	'2021-12-07 11:01:27',	'2021-12-19 14:58:16',	1,	'61bf48883dd45.jpg'),
(3,	1,	3,	'Dune',	'Dune est un roman de science-fiction de l\'écrivain Frank Herbert, publié aux États-Unis en 1965. Il s\'agit du premier roman du cycle de Dune. Publié à l\'origine sous forme de deux publications distinctes dans le magazine Analog en 1963-1964, c\'est le roman de science-fiction le plus vendu au monde.',	'61bddf4fcb3b1.jpg',	'61bde2455efc8.epub',	'2-221-02602-0',	'1965-02-01 19:18:00',	'2021-12-07 11:02:02',	'2021-12-19 14:57:50',	1,	'61bf486e2ef72.jpg'),
(5,	5,	NULL,	'Alice au pays des merveilles',	'Assise dans l\'herbe un jour d\'été, la jeune Alice rêve quand soudain un lapin blanc pressé passe devant elle. Brûlante de curiosité, Alice s\'engouffre derrière lui dans son terrier et se retrouve plongée au pays des merveilles.',	'61bdb05b25fe3.jpg',	'61bda3b2d902a.epub',	NULL,	'1865-07-04 00:00:00',	'2021-12-09 12:54:34',	'2021-12-19 14:58:36',	1,	'61bf489c8e5b2.jpg'),
(6,	14,	NULL,	'Undead Story',	'Les morts-vivants sont partout ! Tout autour de nous ! Aux quatre coins du monde des survivants s\'organisent luttant pour leur survie, les situations tragiques et terrifiantes s\'enchaînent, plongeant humains et morts-vivants dans la terreur de la mort !',	'61bde03becd02.png',	'61b34730a2ee8.epub',	NULL,	'2013-02-25 00:00:00',	'2021-12-10 12:25:20',	'2021-12-18 13:20:59',	0,	NULL),
(7,	14,	NULL,	'Le monde des morts part 2',	'Il y a treize années, les zombies ont envahi notre monde. J’ai perdu tous ceux que j’aimais et j’ai dû apprendre à vivre avec la peur au ventre. La vie s’est reconstruite tant bien que mal, imposant ses toutes nouvelles règles. Notre ville barricadée est synonyme d’espoir. Reconstruire et survivre, sont les deux mots d’ordre. Je dois m’y tenir, pour la ville, pour nous, pour mon fils.',	'61bde0d49427c.jpg',	'61b348617f239.epub',	NULL,	'2015-03-05 00:00:00',	'2021-12-10 12:30:25',	'2021-12-22 16:27:54',	1,	'61c3520aaff30.jpg'),
(8,	13,	NULL,	'Le vampire',	'1816, Villa Diodati, sur les bords du Léman, quelques amis se proposèrent une gageure : écrire en une journée une histoire de fantômes. Parmi eux, Mary Shelley qui écrivit Frankenstein et Lord Byron qui ébaucha une nouvelle : le Vampire.\r\nPolidori, le secrétaire particulier de Byron termina la nouvelle que ce dernier avait abandonnée. \r\nUn des premier vampire de la littérature, déjà sanglant mais aussi persuasif, cynique, hypnotique ?',	'61bde0576b24b.jpg',	'61b34cab1773e.epub',	NULL,	'1819-02-05 00:00:00',	'2021-12-10 12:48:43',	'2021-12-18 13:21:27',	0,	NULL),
(9,	12,	NULL,	'L\'étrange mort de M.Bertin',	'L\'inspecteur Aloysius Pendergast est chez lui, à New York, quand il reçoit un avis de décès. M. Bertin s\'est éteint à l\'âge de 81 ans. Accompagné de Constance Greene, sa protégée, Pendergast se rend à La Nouvelle-Orléans, sur les lieux de son enfance, pour assister à l\'enterrement de celui qui fut son précepteur. Bien qu\'elle semble naturelle, Pendergast ne peut s\'empêcher de trouver étrange la mort de M.\r\nBertin. Comme si elle annonçait l\'imminence d\'un danger... Preston & Child offrent cette nouvelle inédite à leurs lecteurs. L\'occasion unique pour ceux qui ne connaîtraient pas encore l\'inspecteur A. X. L. Pendergast, du FBI, de faire connaissance avec le Sherlock Holmes des temps modernes.',	'61bf35b3ab71d.jpg',	'61b36138d362c.epub',	'978-2-8098-3954-8',	'2020-04-09 00:00:00',	'2021-12-10 14:16:24',	'2021-12-19 13:37:55',	0,	NULL),
(10,	11,	NULL,	'Les derniers hommes',	'Quelques peuples nomades tentent de subsister dans une Europe dévastée par les pollutions chimiques, nucléaires et génétiques. Parmi eux, le peuple de l\'eau. Le seul à pouvoir localiser les sources épargnées par la contamination. L\'avenir de tous dépend des baguettes des sourciers. Et sans eau pure, pas de vie ! Solman le boiteux est né avec le don de clairvoyance. Infaillible juge des âmes, rejeté par les autres, le jeune homme ne peut se confier qu\'à Raïma la guérisseuse.\r\nElle l\'aide à prendre conscience de son pouvoir, lui ouvre les yeux sur les signes qui jalonnent la route du peuple de l\'eau. Des signes qui, à la lueur du Livre interdit, semblent annoncer la fin des derniers hommes.',	'61bdb16376f3a.jpg',	'61b3624d2591c.epub',	'978-2-84626-284-2',	'2010-07-23 00:00:00',	'2021-12-10 14:21:01',	'2021-12-18 10:01:07',	0,	NULL),
(11,	9,	NULL,	'Dark Elements (Tome 1)',	'Layla est un être unique. Non seulement ses baisers sont capables de tuer n\'importe qui ayant une âme, mais elle est aussi la seule représentante de son espèce : mi-gargouille, mi-démon. Or, quand on grandit au sein d\'un clan de Gardiens chargés d\'anéantir les créatures démoniaques pour protéger l\'humanité, mieux vaut faire profil bas et cacher ses sentiments. En particulier auprès du charmant Zayne, qui la voit davantage comme une petite sour.\r\nLorsque Layla rencontre Roth, un démon aussi dangereux que séduisant, la liste de ses priorités change quelque peu. En effet, ce dernier prétend connaître tous ses secrets, notamment celui de ses origines.',	'61bde0edcec8f.jpg',	'61b3682881963.epub',	'9782290239735',	'2020-03-12 00:00:00',	'2021-12-10 14:46:00',	'2021-12-18 13:23:57',	0,	NULL),
(12,	10,	NULL,	'Dans les ténèbres',	'Rouen est la ville aux cent clochers. Quand une cloche est découverte en plein milieu du sol de la cathédrale Notre-Dame, aucune trace ne permet de déterminer par quel miracle elle s’est retrouvée là. D’autant qu’autour de la gigantesque coupole de cuivre et d’étain s’étend une mare de sang.\r\n\r\nDépêché pour résoudre cet intrigant mystère, l’inspecteur Henri Bernes va découvrir que les églises et même les cathédrales n’empêchent en rien le Mal d’étendre son influence ; au contraire, c’est peut-être via ces dernières qu’Il tente de se libérer de ses geôles...',	'61bde10be6993.jpg',	'61b3926856166.epub',	'978-2-37227-066-3',	'2018-10-31 00:00:00',	'2021-12-10 17:46:16',	'2021-12-18 13:24:27',	0,	NULL),
(13,	8,	NULL,	'Contes de noël',	'Assurément tous les petits enfants connaissent cette fête ! Elle est belle, elle est radieuse pour le plus grand nombre. Elle ramène l\'excellent vieux Santa Claus avec des trésors fabuleux entassés dans ses poches immenses et inépuisables. Quelques-uns, hélas ! ne connaissent de ce jour que les privations, plus cruelles par leur contraste avec la joie de tout le monde. Ces malheureux petits pauvres que Santa Claus ne connaît pas, qui ne trouvent jamais, jamais rien dans leur soulier, c\'est aux enfants heureux de les consoler, de se constituer leur Providence visible.',	'61bdb01b588d6.jpg',	'61bda68333550.epub',	'978-2-8247-1427-1',	'1969-02-01 00:02:00',	'2021-12-18 09:14:43',	'2021-12-18 09:55:39',	0,	NULL),
(14,	7,	NULL,	'Le petit chose',	'\'Le Petit Chose\' paraît en feuilleton en 1867. Daudet s\'inspire des souvenirs d\'une jeunesse douloureuse : humiliations à l\'école, mépris pour le petit provençal, expérience de répétiteur au collège et enfin coup de foudre pour une belle jeune femme. L\'écrivain manifeste une tendresse, une pitié et un respect remarquables à l\'égard des malchanceux et des déshérités de la vie. Extrait : Au bout d\'un mois, la vieille Annou tomba malade. Les brouillards la tuaient ; on dut la renvoyer dans le Midi. Cette pauvre fille, qui aimait ma mère à la passion, ne pouvait pas se décider à nous quitter. Elle suppliait qu\'on la gardât, promettant de ne pas mourir. Il fallut l\'embarquer de force. Arrivée dans le Midi, elle s\'y maria de désespoir. Annou partie, on ne prit pas de nouvelle bonne, ce qui me parut le comble de la misère...',	'61bdb0078a21c.jpg',	'61bda728cc40e.epub',	'978-2-8247-0091-5',	'1867-06-07 14:14:00',	'2021-12-18 09:17:28',	'2021-12-18 09:55:19',	0,	NULL),
(15,	6,	NULL,	'Roman d\'un enfant',	'Pierre Loti raconte ici son enfance. Enfance pleine de tendresse, d\'amitié et de mystère. Enfance de petit garçon songeur, vivant dans un mondé d\'irréalités sur lequel l\'éducation n\'a point dé prise, formant sans cesse mille rêvés grandioses et impossibles, mais au travers desquels, déjà, une double vocation s\'éveille... Extrait : Ce que je craignais de voir arriver par là n’avait encore aucune forme précise ; plus tard seulement, mes visions d’enfant prirent figure. Mais la peur n’en était pas moins réelle et m’immobilisait là, les yeux très ouverts, auprès de ce feu qui n’éclairait plus, — quand tout à coup, du côté opposé, par une autre porte, ma mère entra... Oh ! alors je me jetai sur elle ; je me cachai la tête, je m’abîmai dans sa robe : c’était la protection suprême, l’asile où rien n’atteignait plus, le nid des nids où l’on oubliait tout...',	'61bdafddcf7b8.jpg',	'61bda8310816c.epub',	'978-2-8247-1100-3',	'1800-08-03 11:10:00',	'2021-12-18 09:21:53',	'2021-12-18 09:54:37',	0,	'61bdafb8be3cc.jpg'),
(18,	16,	NULL,	'Par-dessus les moulins',	'Qu’est-ce qui me prouve que votre sœur n’a pas menti et que ce bébé est bien l’enfant de mon frère ?\r\nOutrée, Caroline claque la porte derrière Jeremy Revell, le puissant directeur de la fameuse compagnie Revell. Qu’il aille au diable ! il ne vaut certainement pas mieux que le misérable qui a causé la mort de sa sœur. Elle ne lui a rien demandé et se débrouillera bien toute seule pour élever son neveu.\r\nMais Jeremy ne l’entend pas de cette oreille. Imperturbable, insensible aux insultes, en homme habitué à être obéi, il revient à la charge avec une proposition qui ressemble fort à un chantage.\r\nCompte-t-il sur son charme ? Sur son argent ? Ou pense-t-il tout simplement profiter de la détresse de Caroline pour arriver à ses fins ?',	'61bdb65d41f9c.jpg',	'61bdb65d422bb.epub',	NULL,	'1982-01-01 07:00:00',	'2021-12-18 10:22:21',	NULL,	0,	NULL),
(19,	18,	NULL,	'L\'écho d\'un amour',	'Elle l’avait passionnément aimé, et il l’avait trahie.\r\nDepuis, Amanda s’était retirée à Rialto, une petite ville de l’Illinois, dont elle était l’unique médecin. Dévouée à cette population qui l’avait adoptée, elle s’efforçait d’oublier… Mais dans la vie sage d’Amanda, un homme allait tout remettre en cause. Cet homme, elle savait tout de lui – jusqu’à son signe. Et elle ne voulait pas le revoir…\r\nEntre cette sage native du Poissons et ce Lion fougueux, le face à face ne faisait que commencer…',	'61bdb812e8311.jpg',	'61bdb812e84a6.epub',	NULL,	'2003-07-14 09:07:00',	'2021-12-18 10:29:38',	NULL,	0,	NULL),
(20,	19,	NULL,	'Promesse de lumière',	'Quand le directeur de la galerie d’art où elle travaille demande à Jane d’aller interviewer le célèbre photographe Spencer Gallant, elle est ravie. Ne raffole-t-elle pas des tâches délicates ?\r\nUne fois sur place, cet artiste au charme singulier l’impressionne plus qu’elle ne le voudrait. Certes, elle admire son talent… Mais c’est surtout sa proximité qui la trouble…\r\nDès qu’il s’approche d’elle, Jane se sent autre…',	'61bdb9603e05f.jpg',	'61bdb9603e1aa.epub',	'978-2280120470',	'1985-01-01 15:13:00',	'2021-12-18 10:35:12',	NULL,	0,	NULL);

DROP TABLE IF EXISTS `book_category`;
CREATE TABLE `book_category` (
  `book_id` int(11) NOT NULL,
  `category_id` int(11) NOT NULL,
  PRIMARY KEY (`book_id`,`category_id`),
  KEY `IDX_1FB30F9816A2B381` (`book_id`),
  KEY `IDX_1FB30F9812469DE2` (`category_id`),
  CONSTRAINT `FK_1FB30F9812469DE2` FOREIGN KEY (`category_id`) REFERENCES `category` (`id`) ON DELETE CASCADE,
  CONSTRAINT `FK_1FB30F9816A2B381` FOREIGN KEY (`book_id`) REFERENCES `book` (`id`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `book_category` (`book_id`, `category_id`) VALUES
(2,	4),
(3,	2),
(5,	4),
(6,	1),
(7,	1),
(8,	1),
(9,	5),
(10,	4),
(11,	2),
(11,	4),
(12,	1),
(12,	2),
(12,	4),
(13,	6),
(14,	6),
(15,	6),
(18,	3),
(19,	3),
(20,	3);

DROP TABLE IF EXISTS `category`;
CREATE TABLE `category` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  `updated_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  `image` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `category` (`id`, `name`, `created_at`, `updated_at`, `image`) VALUES
(1,	'Horreur',	'2021-12-07 10:55:49',	'2021-12-19 17:48:59',	'61bf708bce48c.jpg'),
(2,	'Fantasie',	'2021-12-07 10:55:56',	'2021-12-19 18:23:53',	'61bf78b9d68e8.jpg'),
(3,	'Romance',	'2021-12-07 10:56:00',	'2021-12-19 17:12:35',	'61bf6803639da.jpg'),
(4,	'Science-Fiction',	'2021-12-07 10:56:09',	'2021-12-19 18:32:55',	'61bf7ad7c48ff.jpg'),
(5,	'Thriller',	'2021-12-07 10:59:10',	NULL,	NULL),
(6,	'Enfant',	'2021-12-18 09:05:38',	NULL,	NULL);

DROP TABLE IF EXISTS `editor`;
CREATE TABLE `editor` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  `updated_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `editor` (`id`, `name`, `created_at`, `updated_at`) VALUES
(1,	'Hachette',	'2021-12-07 10:57:42',	NULL),
(2,	'Poche',	'2021-12-07 10:57:46',	NULL),
(3,	'Dupuis',	'2021-12-07 10:57:50',	NULL);

DROP TABLE IF EXISTS `favorite`;
CREATE TABLE `favorite` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `book_id` int(11) DEFAULT NULL,
  `user_id` int(11) DEFAULT NULL,
  `is_favorite` tinyint(1) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `IDX_68C58ED916A2B381` (`book_id`),
  KEY `IDX_68C58ED9A76ED395` (`user_id`),
  CONSTRAINT `FK_68C58ED916A2B381` FOREIGN KEY (`book_id`) REFERENCES `book` (`id`),
  CONSTRAINT `FK_68C58ED9A76ED395` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `favorite` (`id`, `book_id`, `user_id`, `is_favorite`) VALUES
(3,	2,	1,	1),
(4,	3,	2,	1);

DROP TABLE IF EXISTS `pinnedpage`;
CREATE TABLE `pinnedpage` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `book_id` int(11) DEFAULT NULL,
  `user_id` int(11) DEFAULT NULL,
  `page` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  `updated_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  PRIMARY KEY (`id`),
  KEY `IDX_FA2E797816A2B381` (`book_id`),
  KEY `IDX_FA2E7978A76ED395` (`user_id`),
  CONSTRAINT `FK_FA2E797816A2B381` FOREIGN KEY (`book_id`) REFERENCES `book` (`id`),
  CONSTRAINT `FK_FA2E7978A76ED395` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `pinnedpage` (`id`, `book_id`, `user_id`, `page`, `created_at`, `updated_at`) VALUES
(2,	2,	2,	NULL,	'2021-12-07 11:08:41',	NULL),
(57,	6,	22,	'epubcfi(/6/14[id417]!/4/4/14/2/1:0)',	'2021-12-17 14:23:54',	'2021-12-18 09:16:43'),
(66,	9,	22,	'epubcfi(/6/12[e9782809839548_c001]!/4/2/46/1:0)',	'2021-12-18 09:51:17',	'2021-12-19 10:27:53'),
(67,	5,	22,	'epubcfi(/6/6[chap.xhtml]!/4/2/16/1:0)',	'2021-12-18 09:51:42',	'2021-12-18 09:53:03'),
(68,	13,	22,	'epubcfi(/6/14[html510]!/4/2[calibre_toc_2]/3:0)',	'2021-12-18 09:59:18',	'2021-12-18 09:59:38'),
(69,	2,	22,	'epubcfi(/6/8[html26]!/4/14/2/1:177)',	'2021-12-18 10:04:13',	'2021-12-18 10:04:20'),
(83,	14,	1,	'epubcfi(/6/16[html534]!/4/2[calibre_toc_2]/2/1:0)',	'2021-12-20 07:10:29',	'2021-12-20 07:10:29'),
(84,	8,	1,	'epubcfi(/6/2[title]!/4/2/1:0)',	'2021-12-20 07:10:41',	'2021-12-20 07:10:42'),
(92,	9,	1,	'epubcfi(/6/12[e9782809839548_c001]!/4/2/116/3:67)',	'2021-12-20 11:01:10',	'2021-12-20 11:01:13'),
(93,	5,	62,	'epubcfi(/6/14[chap_0005.xhtml]!/4/2[heading_id_2]/2/2/1:0)',	'2021-12-20 11:38:11',	'2021-12-20 11:38:55'),
(95,	5,	63,	'epubcfi(/6/6[chap.xhtml]!/4/2/14/1:0)',	'2021-12-20 12:19:59',	'2021-12-20 12:22:27'),
(100,	11,	1,	'epubcfi(/6/2[html-cover-page]!/4/1:0)',	'2021-12-21 08:55:03',	'2021-12-21 08:55:04'),
(101,	12,	1,	'epubcfi(/6/2[cover.xhtml]!/4/4/1:0)',	'2021-12-21 08:55:10',	'2021-12-21 08:55:11'),
(102,	10,	1,	'epubcfi(/6/2[cover]!/4/1:0)',	'2021-12-21 08:55:17',	'2021-12-21 08:55:18'),
(109,	3,	19,	'epubcfi(/6/2[html-cover-page]!/4/1:0)',	'2021-12-21 15:13:55',	'2021-12-21 15:13:56'),
(110,	12,	19,	'epubcfi(/6/4[Titre.xhtml]!/4/2/1:0)',	'2021-12-21 15:14:07',	'2021-12-21 15:14:32'),
(111,	6,	19,	'epubcfi(/6/12[id418]!/4/6/76/2/1:0)',	'2021-12-21 15:15:10',	'2021-12-21 15:18:14'),
(112,	18,	19,	'epubcfi(/6/8[id210]!/4/2[toc_id_2]/1:0)',	'2021-12-21 15:15:34',	'2021-12-21 15:15:47'),
(113,	9,	19,	'epubcfi(/6/6[e9782809839548_cop01]!/4/2[pc]/4/1:0)',	'2021-12-21 15:17:27',	'2021-12-21 15:17:38'),
(116,	5,	74,	'epubcfi(/6/10[chap_0003.xhtml]!/4/40/1:0)',	'2021-12-22 17:04:28',	'2021-12-22 17:04:31'),
(117,	3,	74,	'epubcfi(/6/22[p1chap1]!/4/2[chap-005]/8/32/1:240)',	'2021-12-22 17:04:49',	'2021-12-22 17:05:04');

DROP TABLE IF EXISTS `recommendation`;
CREATE TABLE `recommendation` (
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  `updated_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `book_id` int(11) DEFAULT NULL,
  `user_id` int(11) DEFAULT NULL,
  `content` longtext COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `recommendation` tinyint(1) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `IDX_433224D216A2B381` (`book_id`),
  KEY `IDX_433224D2A76ED395` (`user_id`),
  CONSTRAINT `FK_433224D216A2B381` FOREIGN KEY (`book_id`) REFERENCES `book` (`id`),
  CONSTRAINT `FK_433224D2A76ED395` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `recommendation` (`created_at`, `updated_at`, `id`, `book_id`, `user_id`, `content`, `recommendation`) VALUES
('2021-12-15 12:28:09',	NULL,	3,	2,	12,	'C PA FOUFOU',	1);

DROP TABLE IF EXISTS `reset_password`;
CREATE TABLE `reset_password` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL,
  `token` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  PRIMARY KEY (`id`),
  KEY `IDX_B9983CE5A76ED395` (`user_id`),
  CONSTRAINT `FK_B9983CE5A76ED395` FOREIGN KEY (`user_id`) REFERENCES `user` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `reset_password` (`id`, `user_id`, `token`, `created_at`) VALUES
(8,	20,	'61c080ed30b45',	'2021-12-20 13:11:09'),
(9,	20,	'61c0819b5dbfe',	'2021-12-20 13:14:03'),
(10,	20,	'61c0825773b58',	'2021-12-20 13:17:11'),
(11,	20,	'61c0826326bc5',	'2021-12-20 13:17:23'),
(12,	20,	'61c08e4619bea',	'2021-12-20 14:08:06'),
(13,	20,	'61c08ff27da47',	'2021-12-20 14:15:14');

DROP TABLE IF EXISTS `user`;
CREATE TABLE `user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `email` varchar(180) COLLATE utf8mb4_unicode_ci NOT NULL,
  `roles` longtext COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '(DC2Type:json)',
  `password` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `profile_pic` varchar(255) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
  `created_at` datetime NOT NULL COMMENT '(DC2Type:datetime_immutable)',
  `updated_at` datetime DEFAULT NULL COMMENT '(DC2Type:datetime_immutable)',
  PRIMARY KEY (`id`),
  UNIQUE KEY `UNIQ_8D93D649E7927C74` (`email`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

INSERT INTO `user` (`id`, `email`, `roles`, `password`, `name`, `profile_pic`, `created_at`, `updated_at`) VALUES
(1,	'admin@admin.com',	'[\"ROLE_USER\",\"ROLE_ADMIN\"]',	'$2y$13$hKBsI5GHexCwYiqW1P8ItuPG2tQXrOLKtyC4s1m1lwSOyAP.5HWBq',	'admin',	'61bb3773119ab.jpg',	'2021-12-07 09:48:45',	'2021-12-17 14:40:22'),
(2,	'user@user.com',	'[]',	'$2y$13$w7GHVFJuIWdRKwHIxrjqIemav20RPI9QX3ie9b.ikHX1aS3KTc5wK ',	'user',	'61af9aa465fce.jpg',	'2021-12-07 09:50:01',	'2021-12-07 17:32:20'),
(4,	'test@test.com',	'[]',	'$2y$13$TQB1zWyLhtCNTyylFVZ3D.hTmhJupIL3i99Aj8BYMHdEju6YO0Qfy',	'testtest',	'user_default.png',	'2021-12-09 09:58:58',	NULL),
(12,	'bastien@bastien.com',	'[]',	'$2y$13$oPioNp42Ewa22IddwGrCweUUVsObdTn2eBryZQDXEeqRPzcrMj4.O',	'Bastieng',	'user_default.png',	'2021-12-09 14:06:08',	NULL),
(13,	'endive@gmail.com',	'[]',	'$2y$13$emFQo695Im45uju/s/LifOuAvd.5honTYi69Sv7IewNszyrNu4AoG',	'endive',	'user_default.png',	'2021-12-15 13:15:47',	NULL),
(14,	'bon@password.com',	'[]',	'$2y$13$yFUTbybJpm/XnXyds5wA0ezYem3xsWVPnVLP9RQ4FwzYCTX2Emz1m',	'bonpassword',	'user_default.png',	'2021-12-16 09:32:47',	NULL),
(16,	'verifbon@password.com',	'[]',	'$2y$13$/GN.DaVQWl47MPLuhvGp/OVQOO2isqns3NInj4X1b.3En2LgMIkMC',	'verifbonpassword',	'user_default.png',	'2021-12-16 09:35:13',	NULL);
