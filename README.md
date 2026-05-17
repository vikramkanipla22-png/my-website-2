import { useState, useRef } from 'react';
import { motion } from 'motion/react';
import { 
  Menu, X, CheckCircle, Globe, PlaneTakeoff, 
  Briefcase, GraduationCap, Star, MapPin, 
  Phone, Mail, Clock, ChevronRight, Award, ChevronLeft
} from 'lucide-react';

export default function App() {
  return (
    <div className="font-sans text-gray-900 bg-white min-h-screen scroll-smooth">
      <Navbar />
      <main>
        <Hero />
        <Stats />
        <Services />
        <SlidingDestinations />
        <About />
        <Gallery />
        <Testimonials />
        <Contact />
      </main>
      <Footer />
      <WhatsAppButton />
    </div>
  );
}

const fadeIn = {
  hidden: { opacity: 0, y: 20 },
  visible: { opacity: 1, y: 0, transition: { duration: 0.6 } }
};

const staggerContainer = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: { staggerChildren: 0.2 }
  }
};

function SlidingDestinations() {
  const scrollRef = useRef<HTMLDivElement>(null);

  const scroll = (direction: 'left' | 'right') => {
    if (scrollRef.current) {
      const scrollAmount = window.innerWidth > 768 ? 400 : 300;
      scrollRef.current.scrollBy({
        left: direction === 'left' ? -scrollAmount : scrollAmount,
        behavior: 'smooth'
      });
    }
  };

  const destinations = [
    { name: "Paris, France", image: "https://images.unsplash.com/photo-1499856871958-5b9627545d1a?auto=format&fit=crop&q=80&w=2020" },
    { name: "London, UK", image: "https://images.unsplash.com/photo-1513635269975-59663e0ac1ad?auto=format&fit=crop&q=80&w=2070" },
    { name: "Toronto, Canada", image: "https://images.unsplash.com/photo-1518972553974-bc5db04285ad?auto=format&fit=crop&q=80&w=2070" },
    { name: "Sydney, Australia", image: "https://images.unsplash.com/photo-1506973035872-a4ec16b8e8d9?auto=format&fit=crop&q=80&w=2070" },
    { name: "New York, USA", image: "https://images.unsplash.com/photo-1496442226666-8d4d0e62e6e9?auto=format&fit=crop&q=80&w=2070" },
    { name: "Rome, Italy", image: "https://images.unsplash.com/photo-1552832230-c0197dd311b5?auto=format&fit=crop&q=80&w=1996" },
    { name: "Dubai, UAE", image: "https://images.unsplash.com/photo-1512453979798-5ea266f8880c?auto=format&fit=crop&q=80&w=2070" },
    { name: "Tokyo, Japan", image: "https://images.unsplash.com/photo-1503899036084-c55cdd92da26?auto=format&fit=crop&q=80&w=2070" },
    { name: "Auckland, New Zealand", image: "https://images.unsplash.com/photo-1507699622108-4be3abd695ad?auto=format&fit=crop&q=80&w=2071" },
  ];

  return (
    <section className="py-24 bg-slate-50 overflow-hidden relative border-y border-slate-100">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 mb-10 flex flex-col md:flex-row md:justify-between md:items-end gap-6 text-center md:text-left">
         <div>
            <h2 className="text-blue-600 font-semibold tracking-wide uppercase mb-3 text-sm">Top Tourist Destinations</h2>
            <h3 className="text-3xl md:text-4xl lg:text-5xl font-bold text-blue-950 max-w-2xl font-display">Explore Your Dream Destinations</h3>
         </div>
         <div className="hidden md:flex gap-3 shrink-0">
           <button title="Previous" onClick={() => scroll('left')} className="p-3 bg-white rounded-full border border-slate-200 hover:bg-slate-50 hover:border-blue-300 text-blue-900 transition-all shadow-sm">
             <ChevronLeft className="w-6 h-6" />
           </button>
           <button title="Next" onClick={() => scroll('right')} className="p-3 bg-white rounded-full border border-slate-200 hover:bg-slate-50 hover:border-blue-300 text-blue-900 transition-all shadow-sm">
             <ChevronRight className="w-6 h-6" />
           </button>
         </div>
      </div>

      <div className="relative w-full">
        <div 
          ref={scrollRef}
          className="flex gap-6 overflow-x-auto snap-x snap-mandatory pt-4 pb-12 px-4 sm:px-6 lg:px-8 items-center [&::-webkit-scrollbar]:hidden"
          style={{ scrollbarWidth: 'none', msOverflowStyle: 'none' }}
        >
          {destinations.map((dest, idx) => (
            <div key={idx} className="relative w-[280px] md:w-[350px] shrink-0 aspect-[4/5] md:aspect-[3/4] rounded-3xl overflow-hidden snap-center cursor-pointer group/card shadow-lg hover:shadow-2xl transition-all border border-black/5">
              <img src={dest.image} alt={dest.name} className="w-full h-full object-cover transition-transform duration-700 group-hover/card:scale-110" loading="lazy" />
              <div className="absolute inset-0 bg-gradient-to-t from-black/90 via-black/20 to-transparent flex flex-col justify-end p-6 md:p-8 pointer-events-none">
                 <h4 className="text-white text-2xl md:text-3xl font-bold font-display tracking-wide mb-2">{dest.name}</h4>
                 <div className="w-12 h-1 bg-cyan-400 rounded-full transform origin-left transition-all duration-300 group-hover/card:w-24 group-hover/card:bg-blue-400"></div>
              </div>
            </div>
          ))}
        </div>
      </div>
      
      <div className="flex justify-center gap-4 -mt-2 md:hidden">
        <button title="Previous" onClick={() => scroll('left')} className="p-3 bg-white shadow-md rounded-full border border-slate-100 active:bg-slate-50 text-blue-900 transition-all">
          <ChevronLeft className="w-6 h-6" />
        </button>
        <button title="Next" onClick={() => scroll('right')} className="p-3 bg-white shadow-md rounded-full border border-slate-100 active:bg-slate-50 text-blue-900 transition-all">
          <ChevronRight className="w-6 h-6" />
        </button>
      </div>
    </section>
  );
}

function BrandLogo({ className = "w-10 h-10" }: { className?: string }) {
  return (
    <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" className={className}>
      <rect width="48" height="48" rx="14" fill="url(#milap-grad)" />
      {/* M Letter (Milap) */}
      <path d="M14 34V18L24 25.5L34 18V34" stroke="white" strokeWidth="4" strokeLinecap="round" strokeLinejoin="round"/>
      {/* Upward Arrow / Taking off (Overseas / Progress) */}
      <path d="M24 25.5V10M24 10L18 16M24 10L30 16" stroke="#67e8f9" strokeWidth="4" strokeLinecap="round" strokeLinejoin="round"/>
      <defs>
        <linearGradient id="milap-grad" x1="0" y1="0" x2="48" y2="48" gradientUnits="userSpaceOnUse">
           <stop stopColor="#1e3a8a" /> {/* blue-900 */}
           <stop offset="1" stopColor="#3b82f6" /> {/* blue-500 */}
        </linearGradient>
      </defs>
    </svg>
  );
}

function Navbar() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <nav className="fixed w-full bg-white/95 backdrop-blur-md z-50 border-b border-gray-100 shadow-sm">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex justify-between h-20 items-center">
          <div className="flex-shrink-0 flex items-center gap-3">
            <BrandLogo className="h-9 w-9 shadow-sm rounded-[10px]" />
            <span className="font-display font-extrabold text-2xl tracking-widest text-blue-950 uppercase">
              MILAP OVERSEAS
            </span>
          </div>
          
          <div className="hidden md:flex items-center space-x-8">
            <a href="#about" className="text-gray-600 hover:text-blue-600 transition-colors font-medium">About</a>
            <a href="#services" className="text-gray-600 hover:text-blue-600 transition-colors font-medium">Services</a>
            <a href="#success" className="text-gray-600 hover:text-blue-600 transition-colors font-medium">Success Stories</a>
            <a href="#contact" className="bg-blue-600 text-white px-6 py-2.5 rounded-full font-medium hover:bg-blue-700 transition-all shadow-md hover:shadow-lg">
              Free Consultation
            </a>
          </div>

          <div className="md:hidden flex items-center">
            <button onClick={() => setIsOpen(!isOpen)} className="text-gray-600 p-2">
              {isOpen ? <X className="h-6 w-6" /> : <Menu className="h-6 w-6" />}
            </button>
          </div>
        </div>
      </div>

      {/* Mobile menu */}
      {isOpen && (
        <motion.div 
          initial={{ opacity: 0, height: 0 }}
          animate={{ opacity: 1, height: 'auto' }}
          className="md:hidden bg-white border-b border-gray-100"
        >
          <div className="px-4 pt-2 pb-6 space-y-4 shadow-lg">
            <a href="#about" onClick={() => setIsOpen(false)} className="block text-gray-600 hover:text-blue-600 font-medium">About</a>
            <a href="#services" onClick={() => setIsOpen(false)} className="block text-gray-600 hover:text-blue-600 font-medium">Services</a>
            <a href="#success" onClick={() => setIsOpen(false)} className="block text-gray-600 hover:text-blue-600 font-medium">Success Stories</a>
            <a href="#contact" onClick={() => setIsOpen(false)} className="block text-center w-full bg-blue-600 text-white px-6 py-3 rounded-full font-medium mt-4">
              Free Consultation
            </a>
          </div>
        </motion.div>
      )}
    </nav>
  );
}

function Hero() {
  return (
    <section className="relative pt-32 pb-20 lg:pt-48 lg:pb-32 overflow-hidden bg-blue-950 text-white">
      {/* Background Pattern/Overlay */}
      <div className="absolute inset-0 opacity-10">
        <div className="absolute inset-0" style={{ backgroundImage: 'radial-gradient(#ffffff 1px, transparent 1px)', backgroundSize: '24px 24px' }}></div>
      </div>
      
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
        <motion.div 
          initial="hidden"
          animate="visible"
          variants={staggerContainer}
          className="text-center max-w-4xl mx-auto"
        >
          <motion.div variants={fadeIn} className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-blue-900/50 border border-blue-400/20 text-blue-200 text-sm font-medium mb-6">
            <Award className="h-4 w-4" />
            #1 Immigration Consultant in Karnal
          </motion.div>
          
          <motion.h1 variants={fadeIn} className="text-4xl md:text-6xl lg:text-7xl font-bold tracking-tight mb-8 leading-tight">
            Your Journey to a <span className="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-cyan-300">Global Future</span> Starts Here
          </motion.h1>
          
          <motion.p variants={fadeIn} className="text-xl text-blue-100 mb-10 max-w-2xl mx-auto leading-relaxed">
            Expert guidance for study visas, PR, and work permits. We transform your global aspirations into reality with transparent, proven processes.
          </motion.p>
          
          <motion.div variants={fadeIn} className="flex flex-col sm:flex-row gap-4 justify-center">
            <a href="#contact" className="inline-flex items-center justify-center px-8 py-4 text-base font-semibold text-blue-950 bg-white rounded-full hover:bg-gray-100 transition-all shadow-xl hover:shadow-2xl">
              Assess Your Eligibility
              <ChevronRight className="ml-2 h-5 w-5" />
            </a>
            <a href="tel:+919876544321" className="inline-flex items-center justify-center px-8 py-4 text-base font-semibold text-white bg-blue-600/20 border border-blue-400/30 rounded-full hover:bg-blue-600/40 transition-all backdrop-blur-sm">
              <Phone className="mr-2 h-5 w-5" />
              Call +91 98765 44321
            </a>
          </motion.div>
        </motion.div>
      </div>
    </section>
  );
}

function Stats() {
  const stats = [
    { label: "Years Experience", value: "10+", icon: Clock },
    { label: "Visas Approved", value: "5000+", icon: CheckCircle },
    { label: "Partner Universities", value: "50+", icon: GraduationCap },
    { label: "Success Rate", value: "98%", icon: Award },
  ];

  return (
    <div className="relative -mt-12 z-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div className="grid grid-cols-2 md:grid-cols-4 gap-4 bg-white rounded-2xl shadow-xl border border-gray-100 p-6 md:p-8">
        {stats.map((stat, idx) => (
          <div key={idx} className="flex flex-col items-center text-center p-4">
            <div className="h-12 w-12 bg-blue-50 rounded-full flex items-center justify-center mb-4 text-blue-600">
              <stat.icon className="h-6 w-6" />
            </div>
            <div className="text-3xl font-bold text-blue-950 mb-1">{stat.value}</div>
            <div className="text-sm font-medium text-gray-500">{stat.label}</div>
          </div>
        ))}
      </div>
    </div>
  );
}

function Services() {
  const services = [
    {
      title: "Study Visas",
      desc: "Comprehensive guidance for admissions in top universities across Canada, UK, USA, & Australia.",
      icon: GraduationCap,
      color: "bg-purple-50 text-purple-600 border-purple-100"
    },
    {
      title: "PR & Immigration",
      desc: "End-to-end support for Permanent Residency applications with high success rates.",
      icon: Globe,
      color: "bg-blue-50 text-blue-600 border-blue-100"
    },
    {
      title: "Work Permits",
      desc: "Secure international work opportunities with our expert permit consultation and filing.",
      icon: Briefcase,
      color: "bg-emerald-50 text-emerald-600 border-emerald-100"
    },
    {
      title: "Tourist Visas",
      desc: "Hassle-free tourist visa applications so you can travel the world without worries.",
      icon: PlaneTakeoff,
      color: "bg-orange-50 text-orange-600 border-orange-100"
    }
  ];

  return (
    <section id="services" className="py-24 bg-gray-50">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <motion.div 
          initial="hidden"
          whileInView="visible"
          viewport={{ once: true, margin: "-100px" }}
          variants={fadeIn}
          className="text-center max-w-3xl mx-auto mb-16"
        >
          <h2 className="text-blue-600 font-semibold tracking-wide uppercase mb-3">Our Services</h2>
          <h3 className="text-3xl md:text-5xl font-bold text-blue-950">Expert Pathways for Your Goals</h3>
        </motion.div>

        <motion.div 
          initial="hidden"
          whileInView="visible"
          viewport={{ once: true, margin: "-100px" }}
          variants={staggerContainer}
          className="grid md:grid-cols-2 lg:grid-cols-4 gap-8"
        >
          {services.map((service, idx) => (
            <motion.div 
              key={idx} 
              variants={fadeIn}
              className="bg-white rounded-2xl p-8 shadow-sm hover:shadow-xl transition-shadow border border-gray-100 group"
            >
              <div className={`h-14 w-14 rounded-xl flex items-center justify-center mb-6 border ${service.color} group-hover:scale-110 transition-transform`}>
                <service.icon className="h-7 w-7" />
              </div>
              <h4 className="text-xl font-bold text-gray-900 mb-3">{service.title}</h4>
              <p className="text-gray-600 leading-relaxed">{service.desc}</p>
            </motion.div>
          ))}
        </motion.div>
      </div>
    </section>
  );
}

function About() {
  const benefits = [
    "100% Transparent Process with no hidden fees",
    "Certified & Licensed Immigration Agents",
    "Partnered with 50+ Top Global Universities",
    "Pre & Post Departure Assistance"
  ];

  return (
    <section id="about" className="py-24 bg-white overflow-hidden">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="grid lg:grid-cols-2 gap-16 items-center">
          
          <motion.div 
            initial={{ opacity: 0, x: -50 }}
            whileInView={{ opacity: 1, x: 0 }}
            viewport={{ once: true }}
            transition={{ duration: 0.6 }}
            className="relative"
          >
            <div className="rounded-3xl overflow-hidden shadow-2xl relative z-10">
              <img 
                src="https://images.unsplash.com/photo-1523240795612-9a054b0db644?auto=format&fit=crop&q=80&w=2070" 
                alt="Students walking together abroad" 
                className="w-full h-[600px] object-cover"
              />
            </div>
            {/* Decorative badge */}
            <div className="absolute -bottom-8 -right-8 bg-blue-950 text-white p-6 rounded-2xl shadow-xl z-20 w-48 animate-bounce-slow">
              <div className="flex items-center gap-2 mb-2 justify-center">
                <Star className="h-6 w-6 text-yellow-400 fill-current" />
                <span className="text-2xl font-bold">4.9/5</span>
              </div>
              <div className="text-center text-sm font-medium text-blue-200">
                Top Rated Consultant<br/>in Karnal
              </div>
            </div>
            {/* Background blob pattern */}
            <div className="absolute top-10 -left-10 w-full h-full bg-blue-50 rounded-3xl -z-10"></div>
          </motion.div>

          <motion.div 
            initial={{ opacity: 0, x: 50 }}
            whileInView={{ opacity: 1, x: 0 }}
            viewport={{ once: true }}
            transition={{ duration: 0.6 }}
          >
            <h2 className="text-blue-600 font-semibold tracking-wide uppercase mb-3">Why Choose Us</h2>
            <h3 className="text-3xl md:text-5xl font-bold text-blue-950 mb-6 leading-tight">
              Bridging Borders, Building Dreams
            </h3>
            <p className="text-lg text-gray-600 mb-8 leading-relaxed">
              At MILAP OVERSEAS, we don't just process files; we shape careers. 
              Based in the heart of Karnal, we have been the trusted compass for thousands of students and professionals aiming for a better life abroad.
            </p>
            
            <ul className="space-y-4 mb-10">
              {benefits.map((benefit, idx) => (
                <li key={idx} className="flex items-start">
                  <CheckCircle className="h-6 w-6 text-green-500 mr-3 shrink-0" />
                  <span className="text-gray-700 font-medium">{benefit}</span>
                </li>
              ))}
            </ul>

            <a href="#contact" className="inline-flex items-center px-8 py-4 text-base font-semibold text-white bg-blue-600 rounded-full hover:bg-blue-700 transition-all shadow-lg hover:shadow-xl">
              Start Your Process
              <ChevronRight className="ml-2 h-5 w-5" />
            </a>
          </motion.div>

        </div>
      </div>
    </section>
  );
}

function Gallery() {
  return (
    <section id="success" className="py-24 bg-gray-50">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center max-w-3xl mx-auto mb-16">
          <h2 className="text-blue-600 font-semibold tracking-wide uppercase mb-3">Celebrating Success</h2>
          <h3 className="text-3xl md:text-5xl font-bold text-blue-950">A Glimpse of Joyful Journeys</h3>
        </div>

        <motion.div 
          initial={{ opacity: 0, y: 20 }}
          whileInView={{ opacity: 1, y: 0 }}
          viewport={{ once: true }}
          transition={{ duration: 0.6 }}
          className="grid grid-cols-2 md:grid-cols-4 gap-4 auto-rows-[250px]"
        >
          {/* Bento Grid Layout */}
          <div className="col-span-2 row-span-2 rounded-2xl overflow-hidden relative group">
            <img src="https://images.unsplash.com/photo-1523050854058-8df90110c9f1?auto=format&fit=crop&q=80&w=2070" className="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" alt="Students graduating" />
            <div className="absolute inset-0 bg-gradient-to-t from-black/60 via-black/0 to-black/0 flex items-end p-6">
              <p className="text-white font-semibold text-xl">500+ Study Visas This Year</p>
            </div>
          </div>
          
          <div className="col-span-2 md:col-span-1 rounded-2xl overflow-hidden relative group">
            <img src="https://images.unsplash.com/photo-1436491865332-7a61a109cc05?auto=format&fit=crop&q=80&w=2074" className="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" alt="Airplane tail" />
          </div>
          
          <div className="col-span-2 md:col-span-1 rounded-2xl overflow-hidden relative group">
            <img src="https://images.unsplash.com/photo-1554224155-8d04cb21cd6c?auto=format&fit=crop&q=80&w=2070" className="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" alt="Passports" />
          </div>
          
          <div className="col-span-2 rounded-2xl overflow-hidden relative group">
            <img src="https://images.unsplash.com/photo-1541339907198-e08756dedf3f?auto=format&fit=crop&q=80&w=2070" className="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" alt="University campus" />
            <div className="absolute inset-0 bg-gradient-to-t from-black/60 via-black/0 to-black/0 flex items-end p-6">
              <p className="text-white font-semibold text-xl">Top Universities admissions secured</p>
            </div>
          </div>
        </motion.div>
      </div>
    </section>
  );
}

function Testimonials() {
  const reviews = [
    {
      name: "Rahul Sharma",
      type: "Canada PR Approved",
      text: "MILAP OVERSEAS made my Canada PR dream a reality. Their team in Karnal is extremely knowledgeable. The process was completely transparent.",
      rating: 5
    },
    {
      name: "Simran Kaur",
      type: "UK Student Visa",
      text: "I got my admission into a prestigious UK university within weeks! The guidance for the interview and file preparation was top-notch.",
      rating: 5
    },
    {
      name: "Amit Verma",
      type: "Australia Work Permit",
      text: "The dedication of the MILAP team is unmatched. They mapped out the perfect immigration pathway for my family and me.",
      rating: 5
    }
  ];

  return (
    <section className="py-24 bg-blue-950 text-white relative">
      <div className="absolute inset-0 opacity-5 bg-[url('https://www.transparenttextures.com/patterns/cubes.png')] animate-[pulse_10s_ease-in-out_infinite]"></div>
      
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
        <h3 className="text-3xl md:text-4xl font-bold text-center mb-16">Trusted by Thousands</h3>

        <div className="grid md:grid-cols-3 gap-8">
          {reviews.map((review, idx) => (
            <motion.div 
              key={idx}
              initial={{ opacity: 0, y: 30 }}
              whileInView={{ opacity: 1, y: 0 }}
              viewport={{ once: true }}
              transition={{ delay: idx * 0.2 }}
              className="bg-white/10 backdrop-blur-md rounded-2xl p-8 border border-white/20"
            >
              <div className="flex text-yellow-400 mb-4">
                {[...Array(review.rating)].map((_, i) => (
                  <Star key={i} className="h-5 w-5 fill-current" />
                ))}
              </div>
              <p className="text-blue-100 text-lg italic mb-6 leading-relaxed">"{review.text}"</p>
              <div>
                <div className="font-bold text-white font-lg">{review.name}</div>
                <div className="text-blue-300 text-sm">{review.type}</div>
              </div>
            </motion.div>
          ))}
        </div>
      </div>
    </section>
  );
}

function Contact() {
  return (
    <section id="contact" className="py-24 bg-white">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex flex-col lg:flex-row gap-16">
          
          {/* Left: Contact Info */}
          <div className="flex-1">
            <h2 className="text-blue-600 font-semibold tracking-wide uppercase mb-3">Get in touch</h2>
            <h3 className="text-3xl md:text-5xl font-bold text-blue-950 mb-8">Ready to Take the Next Step?</h3>
            <p className="text-gray-600 text-lg mb-12">
              Visit our Karnal office or contact us today for a free profile assessment. Let's make your overseas journey smooth and successful.
            </p>

            <div className="space-y-8">
              <div className="flex items-start">
                <div className="flex-shrink-0 h-14 w-14 bg-blue-50 rounded-2xl flex items-center justify-center border border-blue-100">
                  <MapPin className="h-6 w-6 text-blue-600" />
                </div>
                <div className="ml-6">
                  <h4 className="text-xl font-bold text-gray-900 mb-1">Our Location</h4>
                  <p className="text-gray-600">Model Town Road, Near Old Bus Stand<br/>Karnal, Haryana 132001</p>
                </div>
              </div>

              <div className="flex items-start">
                <div className="flex-shrink-0 h-14 w-14 bg-blue-50 rounded-2xl flex items-center justify-center border border-blue-100">
                  <Phone className="h-6 w-6 text-blue-600" />
                </div>
                <div className="ml-6">
                  <h4 className="text-xl font-bold text-gray-900 mb-1">Phone / WhatsApp</h4>
                  <p className="text-gray-600">+91 98765 44321</p>
                  <p className="text-gray-600">+91 98765 12345</p>
                </div>
              </div>

              <div className="flex items-start">
                <div className="flex-shrink-0 h-14 w-14 bg-blue-50 rounded-2xl flex items-center justify-center border border-blue-100">
                  <Mail className="h-6 w-6 text-blue-600" />
                </div>
                <div className="ml-6">
                  <h4 className="text-xl font-bold text-gray-900 mb-1">Email Us</h4>
                  <p className="text-gray-600">hello@milapoverseas.in</p>
                </div>
              </div>

              <div className="flex items-start">
                <div className="flex-shrink-0 h-14 w-14 bg-blue-50 rounded-2xl flex items-center justify-center border border-blue-100">
                  <Clock className="h-6 w-6 text-blue-600" />
                </div>
                <div className="ml-6">
                  <h4 className="text-xl font-bold text-gray-900 mb-1">Working Hours</h4>
                  <p className="text-gray-600">Mon - Sat: 9:30 AM to 6:30 PM</p>
                  <p className="text-gray-600">Sunday: Closed</p>
                </div>
              </div>
            </div>
          </div>

          {/* Right: Form */}
          <div className="flex-1">
            <div className="bg-white rounded-3xl shadow-2xl p-8 md:p-10 border border-gray-100 relative overflow-hidden">
              {/* Decorative gradient */}
              <div className="absolute top-0 right-0 w-32 h-32 bg-blue-400 opacity-20 blur-[60px] rounded-full point-events-none"></div>
              
              <h3 className="text-2xl font-bold text-blue-950 mb-6">Book a Free Consultation</h3>
              
              <form className="space-y-6" onSubmit={(e) => e.preventDefault()}>
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-2">Full Name</label>
                  <input type="text" className="w-full px-4 py-3 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all" placeholder="John Doe" />
                </div>
                
                <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-2">Phone Number</label>
                    <input type="tel" className="w-full px-4 py-3 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all" placeholder="+91 XXXXX XXXXX" />
                  </div>
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-2">Email Address</label>
                    <input type="email" className="w-full px-4 py-3 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all" placeholder="you@example.com" />
                  </div>
                </div>

                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-2">Service Required</label>
                  <select className="w-full px-4 py-3 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all bg-white text-gray-700">
                     <option>Study Visa</option>
                     <option>PR Application</option>
                     <option>Work Permit</option>
                     <option>Tourist Visa</option>
                     <option>Other / General Enquiry</option>
                  </select>
                </div>

                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-2">Your Message</label>
                  <textarea rows={4} className="w-full px-4 py-3 rounded-xl border border-gray-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all resize-none" placeholder="How can we help you?"></textarea>
                </div>

                <button type="submit" className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 px-8 rounded-xl transition-all shadow-lg hover:shadow-xl hover:-translate-y-1">
                  Submit Application
                </button>
              </form>
            </div>
          </div>

        </div>
      </div>
    </section>
  );
}

function Footer() {
  return (
    <footer className="bg-slate-950 text-slate-400 py-12 border-t border-slate-900">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="grid md:grid-cols-4 gap-8 mb-8">
          <div className="col-span-1 md:col-span-2">
            <div className="flex items-center gap-3 mb-4">
              <BrandLogo className="h-8 w-8 shadow-sm rounded-lg" />
              <span className="font-display font-extrabold text-xl tracking-widest text-white uppercase">
                MILAP OVERSEAS
              </span>
            </div>
            <p className="max-w-xs text-sm">
              Your trusted partner for global aspirations. Licensed immigration & study abroad consultants based in Karnal.
            </p>
          </div>
          <div>
            <h4 className="text-white font-semibold mb-4">Quick Links</h4>
            <ul className="space-y-2 text-sm">
              <li><a href="#home" className="hover:text-blue-400 transition-colors">Home</a></li>
              <li><a href="#about" className="hover:text-blue-400 transition-colors">About Us</a></li>
              <li><a href="#services" className="hover:text-blue-400 transition-colors">Services</a></li>
              <li><a href="#contact" className="hover:text-blue-400 transition-colors">Contact</a></li>
            </ul>
          </div>
          <div>
            <h4 className="text-white font-semibold mb-4">Legal</h4>
            <ul className="space-y-2 text-sm">
              <li><a href="#" className="hover:text-blue-400 transition-colors">Privacy Policy</a></li>
              <li><a href="#" className="hover:text-blue-400 transition-colors">Terms of Service</a></li>
              <li><a href="#" className="hover:text-blue-400 transition-colors">Consultancy License Info</a></li>
            </ul>
          </div>
        </div>
        
        <div className="border-t border-slate-800 pt-8 flex flex-col md:flex-row justify-between items-center gap-4 text-sm">
          <div>&copy; {new Date().getFullYear()} Milap Overseas Karnal. All rights reserved.</div>
          <div className="flex gap-4">
            {/* Social placeholder links */}
            <a href="#" className="hover:text-white transition-colors">Facebook</a>
            <a href="#" className="hover:text-white transition-colors">Instagram</a>
            <a href="#" className="hover:text-white transition-colors">LinkedIn</a>
          </div>
        </div>
      </div>
    </footer>
  );
}

function WhatsAppIcon({ className = "w-6 h-6" }: { className?: string }) {
  return (
    <svg viewBox="0 0 24 24" fill="currentColor" className={className} xmlns="http://www.w3.org/2000/svg">
      <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.888-.788-1.487-1.761-1.66-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51a12.8 12.8 0 0 0-.57-.01c-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413Z"/>
    </svg>
  );
}

function WhatsAppButton() {
  return (
    <a
      href="https://wa.me/919876544321"
      target="_blank"
      rel="noopener noreferrer"
      className="fixed bottom-6 right-6 md:bottom-8 md:right-8 z-50 flex items-center justify-center w-14 h-14 bg-[#25D366] text-white rounded-full shadow-2xl hover:-translate-y-1 hover:shadow-[#25D366]/50 transition-all duration-300 group"
      aria-label="Chat on WhatsApp"
    >
      <span className="absolute inline-flex h-full w-full rounded-full bg-[#25D366] opacity-30 group-hover:animate-ping"></span>
      <WhatsAppIcon className="w-8 h-8 relative z-10" />
    </a>
  );
}