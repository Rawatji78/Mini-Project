import React, { useState, useEffect, useContext, createContext } from 'react';
import { Menu, X, Moon, Sun, Send, MessageCircle, ChevronDown, ChevronRight, Check, Star } from 'lucide-react';

// ============ CONTEXT & STATE MANAGEMENT ============
const ThemeContext = createContext();

const ThemeProvider = ({ children }) => {
  const [isDark, setIsDark] = useState(false);
  
  useEffect(() => {
    if (isDark) {
      document.documentElement.classList.add('dark');
    } else {
      document.documentElement.classList.remove('dark');
    }
  }, [isDark]);
  
  const toggleTheme = () => setIsDark(!isDark);
  return (
    <ThemeContext.Provider value={{ isDark, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

const useTheme = () => useContext(ThemeContext);

// ============ REUSABLE COMPONENTS ============

const Button = ({ children, variant = 'primary', size = 'md', className = '', onClick }) => {
  const baseStyle = 'font-semibold rounded-lg transition-all duration-300 transform hover:scale-105 active:scale-95';
  const variants = {
    primary: 'bg-blue-600 text-white hover:bg-blue-700 shadow-lg hover:shadow-xl',
    secondary: 'bg-gray-200 text-gray-900 hover:bg-gray-300 dark:bg-gray-700 dark:text-white',
    outline: 'border-2 border-blue-600 text-blue-600 hover:bg-blue-50 dark:hover:bg-blue-900/20',
  };
  const sizes = {
    sm: 'px-3 py-1 text-sm',
    md: 'px-6 py-3 text-base',
    lg: 'px-8 py-4 text-lg',
  };
  return (
    <button className={`${baseStyle} ${variants[variant]} ${sizes[size]} ${className}`} onClick={onClick}>
      {children}
    </button>
  );
};

const Card = ({ children, className = '', hover = true }) => {
  const { isDark } = useTheme();
  const baseStyle = `${hover ? 'hover:shadow-xl hover:-translate-y-1 transition-all duration-300' : ''} rounded-xl p-6 ${isDark ? 'bg-gray-800' : 'bg-white'} shadow-lg`;
  return <div className={`${baseStyle} ${className}`}>{children}</div>;
};

// ============ NAVBAR ============
const Navbar = () => {
  const [isOpen, setIsOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);
  const { isDark, toggleTheme } = useTheme();

  useEffect(() => {
    const handleScroll = () => setScrolled(window.scrollY > 50);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const links = ['Home', 'About', 'Services', 'Pricing', 'Contact'];
  const scrollToSection = (section) => {
    const element = document.getElementById(section.toLowerCase());
    element?.scrollIntoView({ behavior: 'smooth' });
    setIsOpen(false);
  };

  return (
    <nav className={`fixed w-full z-50 transition-all duration-300 ${scrolled ? (isDark ? 'bg-gray-900/95 backdrop-blur-md' : 'bg-white/95 backdrop-blur-md shadow-lg') : 'bg-transparent'}`}>
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex justify-between items-center h-16 sm:h-20">
          <div className="flex-shrink-0">
            <h1 className={`text-2xl font-bold bg-gradient-to-r from-blue-600 to-cyan-600 bg-clip-text text-transparent`}>
              ModernBiz
            </h1>
          </div>

          {/* Desktop Menu */}
          <div className="hidden md:flex items-center gap-8">
            {links.map(link => (
              <button key={link} onClick={() => scrollToSection(link)} className={`font-medium transition-colors hover:text-blue-600 ${isDark ? 'text-gray-200' : 'text-gray-700'}`}>
                {link}
              </button>
            ))}
          </div>

          {/* Controls */}
          <div className="flex items-center gap-4">
            <button onClick={toggleTheme} className="p-2 rounded-lg hover:bg-gray-200 dark:hover:bg-gray-700 transition-colors">
              {isDark ? <Sun size={20} /> : <Moon size={20} />}
            </button>
            <button onClick={() => setIsOpen(!isOpen)} className="md:hidden p-2 rounded-lg hover:bg-gray-200 dark:hover:bg-gray-700">
              {isOpen ? <X size={24} /> : <Menu size={24} />}
            </button>
          </div>
        </div>

        {/* Mobile Menu */}
        {isOpen && (
          <div className={`md:hidden pb-4 space-y-2 ${isDark ? 'bg-gray-800' : 'bg-gray-50'}`}>
            {links.map(link => (
              <button key={link} onClick={() => scrollToSection(link)} className="block w-full text-left px-4 py-2 rounded-lg hover:bg-blue-100 dark:hover:bg-blue-900/50 transition-colors">
                {link}
              </button>
            ))}
          </div>
        )}
      </div>
    </nav>
  );
};

// ============ HERO SECTION ============
const HeroSection = () => {
  const { isDark } = useTheme();
  const [animatedText, setAnimatedText] = useState('');
  const fullText = 'Transform Your Business';

  useEffect(() => {
    let index = 0;
    const interval = setInterval(() => {
      if (index <= fullText.length) {
        setAnimatedText(fullText.slice(0, index));
        index++;
      } else clearInterval(interval);
    }, 80);
    return () => clearInterval(interval);
  }, []);

  return (
    <section id="home" className={`relative min-h-screen pt-20 px-4 sm:px-6 lg:px-8 flex items-center overflow-hidden ${isDark ? 'bg-gray-900' : 'bg-gradient-to-br from-blue-50 to-cyan-50'}`}>
      {/* Animated Background */}
      <div className="absolute inset-0 overflow-hidden">
        <div className="absolute w-96 h-96 bg-blue-400 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-pulse -top-20 -left-20"></div>
        <div className="absolute w-96 h-96 bg-cyan-400 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-pulse -bottom-20 -right-20"></div>
      </div>

      <div className="relative max-w-7xl mx-auto grid md:grid-cols-2 gap-12 items-center w-full">
        <div className="space-y-6 z-10">
          <h1 className="text-5xl sm:text-6xl md:text-7xl font-bold leading-tight">
            <span className="bg-gradient-to-r from-blue-600 via-cyan-600 to-blue-600 bg-clip-text text-transparent">
              {animatedText}
            </span>
            <span className="animate-pulse">_</span>
          </h1>
          <p className={`text-lg sm:text-xl leading-relaxed ${isDark ? 'text-gray-300' : 'text-gray-600'}`}>
            Unlock your business potential with cutting-edge solutions designed for modern enterprises.
          </p>
          <div className="flex flex-col sm:flex-row gap-4 pt-4">
            <Button size="lg" onClick={() => document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth' })}>
              Get Started <ChevronRight className="ml-2" size={20} />
            </Button>
            <Button variant="outline" size="lg">Learn More</Button>
          </div>
        </div>

        {/* Hero Animation */}
        <div className="relative h-96 sm:h-full hidden md:block">
          <div className="absolute inset-0 bg-gradient-to-br from-blue-500 to-cyan-500 rounded-3xl opacity-20 animate-bounce"></div>
          <div className="absolute inset-8 bg-gradient-to-br from-blue-600 to-cyan-600 rounded-2xl opacity-30 animate-pulse"></div>
          <div className="absolute inset-16 bg-gradient-to-br from-white/10 to-transparent rounded-2xl backdrop-blur-sm"></div>
        </div>
      </div>

      {/* Scroll Indicator */}
      <div className="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce">
        <ChevronDown size={24} className={isDark ? 'text-gray-400' : 'text-gray-600'} />
      </div>
    </section>
  );
};

// ============ SERVICES SECTION ============
const ServicesSection = () => {
  const { isDark } = useTheme();
  const services = [
    { icon: '🚀', title: 'Strategy', desc: 'Data-driven business strategy' },
    { icon: '💻', title: 'Development', desc: 'Custom software solutions' },
    { icon: '📊', title: 'Analytics', desc: 'Real-time insights & reporting' },
    { icon: '🔒', title: 'Security', desc: 'Enterprise-grade protection' },
    { icon: '☁️', title: 'Cloud', desc: 'Scalable cloud infrastructure' },
    { icon: '🤝', title: 'Support', desc: '24/7 dedicated support' },
  ];

  return (
    <section id="services" className={`py-20 px-4 sm:px-6 lg:px-8 ${isDark ? 'bg-gray-800' : 'bg-white'}`}>
      <div className="max-w-7xl mx-auto">
        <div className="text-center mb-16">
          <h2 className="text-4xl sm:text-5xl font-bold mb-4">Our Services</h2>
          <p className={`text-lg ${isDark ? 'text-gray-400' : 'text-gray-600'}`}>Comprehensive solutions for your business needs</p>
        </div>

        <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-8">
          {services.map((service, i) => (
            <Card key={i} className="text-center group cursor-pointer">
              <div className="text-5xl mb-4 transform group-hover:scale-125 transition-transform">{service.icon}</div>
              <h3 className="text-2xl font-bold mb-2">{service.title}</h3>
              <p className={isDark ? 'text-gray-400' : 'text-gray-600'}>{service.desc}</p>
            </Card>
          ))}
        </div>
      </div>
    </section>
  );
};

// ============ PRICING CALCULATOR ============
const PricingCalculator = () => {
  const { isDark } = useTheme();
  const [users, setUsers] = useState(10);
  const [features, setFeatures] = useState(2);
  
  const basePrice = 99;
  const userPrice = users * 5;
  const featurePrice = features * 50;
  const total = basePrice + userPrice + featurePrice;

  return (
    <Card className={`mt-12 max-w-2xl mx-auto ${isDark ? 'bg-gradient-to-br from-gray-800 to-gray-700' : 'bg-gradient-to-br from-blue-50 to-cyan-50'}`}>
      <h3 className="text-3xl font-bold mb-8 text-center">Price Estimator</h3>
      
      <div className="space-y-8">
        <div>
          <label className="block text-lg font-semibold mb-3">Team Size: <span className="text-blue-600">{users} users</span></label>
          <input type="range" min="1" max="100" value={users} onChange={(e) => setUsers(Number(e.target.value))} className="w-full h-2 bg-gray-300 rounded-lg appearance-none cursor-pointer" />
          <div className="flex justify-between text-sm mt-2 text-gray-500">
            <span>1 user</span>
            <span>100 users</span>
          </div>
        </div>

        <div>
          <label className="block text-lg font-semibold mb-3">Premium Features: <span className="text-blue-600">{features}</span></label>
          <input type="range" min="0" max="5" value={features} onChange={(e) => setFeatures(Number(e.target.value))} className="w-full h-2 bg-gray-300 rounded-lg appearance-none cursor-pointer" />
          <div className="flex justify-between text-sm mt-2 text-gray-500">
            <span>0 features</span>
            <span>5 features</span>
          </div>
        </div>

        <div className={`p-6 rounded-xl ${isDark ? 'bg-gray-900' : 'bg-white'} border-2 border-blue-500`}>
          <div className="space-y-3 mb-4">
            <div className="flex justify-between text-sm"><span>Base Package</span><span>${basePrice}</span></div>
            <div className="flex justify-between text-sm"><span>{users} Users × $5</span><span>${userPrice}</span></div>
            <div className="flex justify-between text-sm"><span>{features} Features × $50</span><span>${featurePrice}</span></div>
            <div className="border-t pt-3 flex justify-between text-2xl font-bold text-blue-600">
              <span>Total</span>
              <span>${total}/month</span>
            </div>
          </div>
          <Button className="w-full">Subscribe Now</Button>
        </div>
      </div>
    </Card>
  );
};

// ============ TESTIMONIALS CAROUSEL ============
const TestimonialsCarousel = () => {
  const { isDark } = useTheme();
  const [current, setCurrent] = useState(0);
  const testimonials = [
    { name: 'Alex Johnson', company: 'TechCorp', text: 'Outstanding service and results!' },
    { name: 'Sarah Lee', company: 'DataSys', text: 'Transformed our entire business.' },
    { name: 'Mike Chen', company: 'CloudNet', text: 'Best investment we ever made.' },
  ];

  return (
    <section className={`py-20 px-4 sm:px-6 lg:px-8 ${isDark ? 'bg-gray-900' : 'bg-gray-100'}`}>
      <div className="max-w-7xl mx-auto">
        <h2 className="text-4xl font-bold text-center mb-16">What Our Clients Say</h2>
        
        <div className={`${isDark ? 'bg-gray-800' : 'bg-white'} rounded-2xl p-8 sm:p-12 shadow-xl max-w-3xl mx-auto`}>
          <div className="flex gap-1 mb-6">
            {[...Array(5)].map((_, i) => (
              <Star key={i} size={20} className="fill-yellow-400 text-yellow-400" />
            ))}
          </div>
          <p className={`text-lg sm:text-xl mb-8 ${isDark ? 'text-gray-300' : 'text-gray-700'}`}>
            "{testimonials[current].text}"
          </p>
          <div className="flex justify-between items-center">
            <div>
              <p className="font-bold">{testimonials[current].name}</p>
              <p className={`text-sm ${isDark ? 'text-gray-400' : 'text-gray-500'}`}>{testimonials[current].company}</p>
            </div>
            <div className="flex gap-2">
              <button onClick={() => setCurrent((current - 1 + testimonials.length) % testimonials.length)} className="p-2 hover:bg-gray-200 dark:hover:bg-gray-700 rounded-lg">←</button>
              <button onClick={() => setCurrent((current + 1) % testimonials.length)} className="p-2 hover:bg-gray-200 dark:hover:bg-gray-700 rounded-lg">→</button>
            </div>
          </div>
        </div>
      </div>
    </section>
  );
};

// ============ FAQ SECTION ============
const FAQSection = () => {
  const { isDark } = useTheme();
  const [expandedFAQ, setExpandedFAQ] = useState(0);
  const faqs = [
    { q: 'How do I get started?', a: 'Sign up, choose a plan, and our team will guide you through setup.' },
    { q: 'What support is available?', a: '24/7 email and chat support with premium plans.' },
    { q: 'Can I switch plans?', a: 'Yes, upgrade or downgrade anytime with prorated billing.' },
    { q: 'Is data secure?', a: 'We use enterprise-grade encryption and compliance standards.' },
  ];

  return (
    <section className={`py-20 px-4 sm:px-6 lg:px-8 ${isDark ? 'bg-gray-800' : 'bg-white'}`}>
      <div className="max-w-4xl mx-auto">
        <h2 className="text-4xl font-bold text-center mb-16">Frequently Asked Questions</h2>
        
        <div className="space-y-4">
          {faqs.map((faq, i) => (
            <div key={i} onClick={() => setExpandedFAQ(expandedFAQ === i ? -1 : i)} className={`cursor-pointer p-6 rounded-lg transition-all ${expandedFAQ === i ? (isDark ? 'bg-blue-900/50' : 'bg-blue-50') : (isDark ? 'bg-gray-700' : 'bg-gray-100')} ${expandedFAQ === i ? 'ring-2 ring-blue-500' : ''}`}>
              <div className="flex justify-between items-center">
                <p className="font-semibold text-lg">{faq.q}</p>
                <ChevronDown size={20} className={`transition-transform ${expandedFAQ === i ? 'rotate-180' : ''}`} />
              </div>
              {expandedFAQ === i && <p className={`mt-4 ${isDark ? 'text-gray-300' : 'text-gray-600'}`}>{faq.a}</p>}
            </div>
          ))}
        </div>
      </div>
    </section>
  );
};

// ============ CONTACT SECTION ============
const ContactSection = () => {
  const { isDark } = useTheme();
  const [formData, setFormData] = useState({ name: '', email: '', message: '' });
  const [submitted, setSubmitted] = useState(false);

  const handleSubmit = async (e) => {
    e.preventDefault();
    console.log('Form submitted:', formData);
    setSubmitted(true);
    setTimeout(() => {
      setSubmitted(false);
      setFormData({ name: '', email: '', message: '' });
    }, 3000);
  };

  return (
    <section id="contact" className={`py-20 px-4 sm:px-6 lg:px-8 ${isDark ? 'bg-gray-900' : 'bg-gray-100'}`}>
      <div className="max-w-4xl mx-auto">
        <h2 className="text-4xl font-bold text-center mb-4">Get In Touch</h2>
        <p className={`text-center mb-12 ${isDark ? 'text-gray-400' : 'text-gray-600'}`}>We'd love to hear from you. Send us a message!</p>

        <Card className="max-w-2xl mx-auto">
          {submitted && (
            <div className="mb-6 p-4 bg-green-100 dark:bg-green-900/50 text-green-700 dark:text-green-300 rounded-lg flex items-center gap-2">
              <Check size={20} /> Message sent successfully!
            </div>
          )}
          
          <div className="space-y-6">
            <div>
              <label className="block text-sm font-semibold mb-2">Name</label>
              <input
                type="text"
                value={formData.name}
                onChange={(e) => setFormData({...formData, name: e.target.value})}
                className={`w-full px-4 py-3 rounded-lg border-2 transition-all ${isDark ? 'bg-gray-700 border-gray-600 text-white' : 'bg-gray-50 border-gray-300'} focus:border-blue-500 focus:outline-none`}
                placeholder="Your Name"
              />
            </div>

            <div>
              <label className="block text-sm font-semibold mb-2">Email</label>
              <input
                type="email"
                value={formData.email}
                onChange={(e) => setFormData({...formData, email: e.target.value})}
                className={`w-full px-4 py-3 rounded-lg border-2 transition-all ${isDark ? 'bg-gray-700 border-gray-600 text-white' : 'bg-gray-50 border-gray-300'} focus:border-blue-500 focus:outline-none`}
                placeholder="your@email.com"
              />
            </div>

            <div>
              <label className="block text-sm font-semibold mb-2">Message</label>
              <textarea
                value={formData.message}
                onChange={(e) => setFormData({...formData, message: e.target.value})}
                className={`w-full px-4 py-3 rounded-lg border-2 transition-all h-32 resize-none ${isDark ? 'bg-gray-700 border-gray-600 text-white' : 'bg-gray-50 border-gray-300'} focus:border-blue-500 focus:outline-none`}
                placeholder="Your message..."
              />
            </div>

            <Button size="lg" className="w-full" onClick={handleSubmit}>
              <Send size={20} className="mr-2 inline" /> Send Message
            </Button>
          </div>
        </Card>
      </div>
    </section>
  );
};

// ============ FOOTER ============
const Footer = () => {
  const { isDark } = useTheme();
  return (
    <footer className={`${isDark ? 'bg-gray-900 border-gray-800' : 'bg-gray-900 border-gray-800'} border-t py-12 px-4 sm:px-6 lg:px-8`}>
      <div className="max-w-7xl mx-auto">
        <div className="grid sm:grid-cols-2 lg:grid-cols-4 gap-8 mb-8">
          <div>
            <h3 className="text-white font-bold mb-4">ModernBiz</h3>
            <p className="text-gray-400 text-sm">Transforming businesses with modern solutions.</p>
          </div>
          <div>
            <h4 className="text-white font-semibold mb-4">Product</h4>
            <ul className="space-y-2 text-gray-400 text-sm"><li><a href="#" className="hover:text-blue-400">Features</a></li><li><a href="#" className="hover:text-blue-400">Pricing</a></li></ul>
          </div>
          <div>
            <h4 className="text-white font-semibold mb-4">Company</h4>
            <ul className="space-y-2 text-gray-400 text-sm"><li><a href="#" className="hover:text-blue-400">About</a></li><li><a href="#" className="hover:text-blue-400">Blog</a></li></ul>
          </div>
          <div>
            <h4 className="text-white font-semibold mb-4">Connect</h4>
            <ul className="space-y-2 text-gray-400 text-sm"><li><a href="#" className="hover:text-blue-400">Twitter</a></li><li><a href="#" className="hover:text-blue-400">LinkedIn</a></li></ul>
          </div>
        </div>
        <div className="border-t border-gray-800 pt-8 text-center text-gray-400 text-sm">
          <p>&copy; 2024 ModernBiz. All rights reserved.</p>
        </div>
      </div>
    </footer>
  );
};

// ============ MAIN APP ============
export default function App() {
  return (
    <ThemeProvider>
      <div className="min-h-screen bg-white dark:bg-gray-900 text-gray-900 dark:text-white transition-colors duration-300">
        <Navbar />
        <HeroSection />
        <ServicesSection />
        <PricingCalculator />
        <TestimonialsCarousel />
        <FAQSection />
        <ContactSection />
        <Footer />
      </div>
    </ThemeProvider>
  );
}
