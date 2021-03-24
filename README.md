# User Interface Demonstration of `plotmm`

Our mixture model visual toolbox includes several tidy functions that allow for streamlined and clean production of mixture model visualizations. The core functions are \texttt{plot\_mm()}, \texttt{plot\_cut\_point()}, and \texttt{plot\_mix\_comps()}, though others are also available in the package.\footnote{As noted in the package documentation, other ``non-core" functions are included mostly to bridge between the more constrained predecessor package, \texttt{plotGMM}, and the currently vastly expanded package, \texttt{plotmm} detailed herein.} In this section, we demonstrate these main functions using both real and simulated data.

\subsection{\texttt{plot\_mm()}}

The \texttt{plot\_mm()} function is the core of the package, and plots the density of the data space with overlaid component curves for \texttt{k} components from the fit mixture model. The package supports the previously identified models mostly from the \texttt{mixtools} package, with some support for \texttt{EMCluster} and \texttt{flexmix} model objects.\footnote{\textit{Note}: as the package is under active development, though stably released, we anticipate much wider support for more model objects and specifications in near-future versions of the package.}

For use, users simply pass the model object to the first argument, as well as an optional argument for the number of components $k$ to the second argument.\footnote{Note: users visualizing \texttt{EMCluster} objects must also pass the name of the data frame to the function} Importantly, as the second argument, $k$, is optional, the function will automatically detect the number of clusters based on the supplied model object. The result is a high-quality visualization of the data space and overlaid estimated component curves. 

For example, see a simple case with a univariate Gaussian mixture model in Figure \ref{figure:one}, using Fisher's Iris dataset: \\

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.4]{one.png}
	\caption{Univariate Gaussian Mixture Model}
	\label{figure:one} 
\end{figure}


Now, consider a bivariate Gaussian case from both \texttt{mixtools} and \texttt{EMCluster} in Figures \ref{figure:four} and \ref{figure:three} respectively. Each are for different sample datasets. Note that the bivariate cases incorporate two features, which the package treats jointly as well as independently. All three figures are rendered in a single plot. There are additional options and functions to layer to change the ordering, labels, colors, spacing, and so on if so desired. 

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.4]{four.png}
	\caption{Bivariate Gaussian Mixture Model mixtools Object}
	\label{figure:four} 
\end{figure}

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.4]{three.png}
	\caption{Bivariate Gaussian Mixture Model EMCluster Object}
	\label{figure:three} 
\end{figure}

Also, other non-normal distributions are also supported such as the gamma distribution previously discussed. See this case in Figure \ref{figure:five}. \\

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.4]{five.png}
	\caption{Gamma Mixture Model}
	\label{figure:five} 
\end{figure}

\clearpage

\subsection{\texttt{plot\_cut\_point()}}

Mixture models can also be used to derive cut points in some data space, which is the point of greatest separation between the clusters. This is a common application of mixture models \citep{benaglia2009mixtools}. The \texttt{plot\_cut\_point()} function allows the user to plot these cut points from mixture models. Similar to \texttt{plot\_mm()}, users simply pass a model object to the function's first argument, with a second argument allowing for an optional plot, with the default option set to \texttt{TRUE}. If \texttt{plot $=$ FALSE}, only the numeric value of the cut point is computed and returned. Finally, though more custom color options are possible through layering additional functions as previously discussed, there is a built in set of color palettes allowing the user to locally change colors. This third argument, \texttt{color}, includes three options: an interpolated scale from blue to red via the \texttt{amerika} package \citep{am}; the ``Rushmore1'' palette via the \texttt{wesanderson} package \citep{ram2015wesanderson}; and a grayscale default option. All of these color options, as well as a demonstration of the ease of adding custom labels and changing default settings are included in Figure \ref{figure:outcut} using the ``Old Faithful'' sample dataset. \\

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.35]{cutpoints}
	\caption{Visual Output via \texttt{plot\_cut\_point()}}
	\label{figure:outcut} 
\end{figure}

\subsection{\texttt{plot\_mix\_comps()}}

Finally, the package includes a powerful helper function, \texttt{plot\_mix\_comps()}, to allow for further customization of visual mixture model output. This function is also used in the core \texttt{plot\_mm()} function. The \texttt{plot\_mix\_comps()} function works by computing and then constraining the parameters that are overlaid. This function is powerful because it is flexible to accommodate \textit{any} mixture model object, not just those from the \texttt{mixtools}, \texttt{EMCluster}, or \texttt{flexmix} packages. The result is custom, publication-ready plot, though more code is needed for a custom plot than required of the main \texttt{plot\_mm()} function. For example, most common use of this function in custom applications would be passing it to the \texttt{fun} argument within the \texttt{stat\_function()} function in a \texttt{ggplot2} object. The result of this type of application is shown in Figure \ref{figure:outcomps}. \\

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.4]{outcomps}
	\caption{Custom Plot with \texttt{plot\_mix\_comps()}}
	\label{figure:outcomps} 
\end{figure}

\section{Comparison to Other Packages}

The value of the package can also be seen in direct comparison with plotting options from existing packages. For example, using the same data, Figure \ref{figure:e1} is using the \texttt{plotem()} function from the \texttt{EMCluster} package, and Figure \ref{figure:p1} is using our tidy software for a much more elegant rendering of the same configuration.

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.3]{e1.png}
	\caption{Plot with \texttt{EMCluster}}
	\label{figure:e1} 
\end{figure}

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.3]{p1.png}
	\caption{Plot with \texttt{plotmm} Tidy Approach}
	\label{figure:p1} 
\end{figure}

As a final comparison, we compare our approach to the \texttt{mixtools} plotting options. The default plotting option for a univariate Gaussian mixture model fit via \texttt{mixtools} is to plot the log-likelihood over each iteration of the model (given that the EM algorithm is iterative). While valuable information, this base plotting option is not intuitive, nor is it substantively useful in visually presenting results from the fit mixture model. Further, the plot is in base R, which is less visually appealing. See this plot for the clustering configuration for the Fisher Iris data set in Figure \ref{figure:m2}.  

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.3]{m2.png}
	\caption{Plot of Fisher Iris Solution via \texttt{mixtools}}
	\label{figure:m2} 
\end{figure}

Our approach shown in Figure \ref{figure:p2}, instead, plots the observed data density, with the estimated component curves overlaid. This is a much more straightforward, intuitive, and visually appealing look at the results from the same model. 

\begin{figure}[htbp]
	\centering
	\includegraphics[scale=.3]{p2.png}
	\caption{Plot of Fisher Iris Solution via \texttt{plotmm} Tidy Approach}
	\label{figure:p2} 
\end{figure}
